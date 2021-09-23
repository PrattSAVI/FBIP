<script>
	import LeafletMap from './Map.svelte'
	import HomeButton from './Home.svelte'
	import LayerButton from './LayerButton.svelte'
	import {onMount} from 'svelte'
	import GeoJson from './Geojson.svelte';
	import GeoJsonBorder from './GeojsonBorder.svelte';
	import InfoPanel from './InfoPanel.svelte';
	import Legend from './Legend.svelte';
	import LegendSmall from './Legend_Small.svelte';
	import ShrunkPanel from './ShrunkPanel.svelte';

	//Retrieve Data from Github Repo
	const url_lots = "https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/data/BIP_FinalLots.geojson";
	const url_border = "https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/data/BIP_lines_4326.geojson";

	let active_data;

	//This gets filled with loadaed data to highlight
	let data = {
		bip:[],
		border:[],
	}

	//Load Data
	onMount(async () => {
		const res = await fetch( url_lots );
		let data_lots = await res.json();
		data.bip = data_lots.features;

		const res2 = await fetch( url_border );
		let border_lots = await res2.json();
		data.border = border_lots.features;
	});

	//Handle Clicked Geojson Object, Point or Polygon. Returns active Polygon Object
	function handleMessage(e){

		//Bring Panel Back
		if (shrunk){
			shrunk = !shrunk;
			document.getElementsByClassName('legend')[0].style.visibility = "hidden";
		}

		//Get clicked polygons unique ID
		 let active = e.detail.active;
		 let obj_id = active._path.id
		 obj_id = obj_id.split(" ")[0] //Onject has multiple IDs. 0 is the unique

		 //Filter data by unique ID to retireve active polygon from the GeoJSON data not HTML object. 
		active_data = data.bip.filter(function(feature){
			let blocklot = String(feature.properties.Block) + String(feature.properties.Lot);
			if( blocklot === obj_id ){
				return true
			}else{
				return false
			}
		})
	}

	function handleClick(e){
		active_data = null;
		let active = document.getElementsByClassName("active")[0];
		if (active){
			active.className.baseVal = "leaflet-interactive"
		}
	}

	let shrunk = false;
    function handleShrunk(event){
		shrunk = !shrunk;
		if (shrunk == true){
			document.getElementsByClassName('legend')[0].style.visibility = "visible";
			document.getElementsByClassName('legend')[0].style.bottom = "65px";
		} else{
			document.getElementsByClassName('legend')[0].style.visibility = "hidden";
		}
	}

	import ResizeObserver from "svelte-resize-observer";
	let width;
	let height;
	let ratio;
	let islandscape = false;
	function setShrunk(e){
		width = e.detail.clientWidth;
		height = e.detail.clientHeight;
		ratio = width/height;

		if (width > 689 ){
			shrunk = false;
			document.getElementsByClassName('legend')[0].style.visibility = "visible";
			document.getElementsByClassName('legend')[0].style.bottom = "15px";
		}else{
			//If size is smaller the 689
			if (shrunk == true){ //and shrunk
				document.getElementsByClassName('legend')[0].style.visibility = "visible";
				document.getElementsByClassName('legend')[0].style.bottom = "50px";
			} else{
				document.getElementsByClassName('legend')[0].style.visibility = "hidden";
			}
		}

		//Mobile on Landscape
		//islandscape defines legend size. 
		if( (ratio > 1) & (height < 600) ){
			if (document.getElementsByClassName('legend')[0].style.visibility === 'visible'){
				document.getElementsByClassName('legend')[0].style.visibility = "hidden";
			} 
			islandscape = true;
		}
		else{
			islandscape = false;
		}
	}


</script>

<svelte:head>
	<link rel="stylesheet" href="https://use.typekit.net/kjc8ltt.css">
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet-easybutton@2/src/easy-button.css">
	<script src="https://cdn.jsdelivr.net/npm/leaflet-easybutton@2/src/easy-button.js"></script>
</svelte:head>

{#if data.border.length > 0 }
	<div class="two-column">
		<div class="left-panel">
			<LeafletMap >
				<HomeButton on:homebutton={handleClick}/>
				<LayerButton />
				<GeoJson on:message={handleMessage} geojson={data.bip} />
				<GeoJsonBorder geojson={data.border} />
				<!--Legend Size is dependent on Mobile-->
				{#key islandscape}
					{#if islandscape == false}
						<Legend />
					{:else}
						<LegendSmall />
					{/if}
				{/key}
			</LeafletMap>
		</div>

		<!-- If the shrink button is pressed, show a different panel-->
		{#if shrunk == false}
			<div class="right-panel">

				<div class="shrink" on:click={handleShrunk}>
					&#10094;
				</div>

				<InfoPanel {active_data}/>
			</div>
		{:else}
			<div class="right-panel shrunk">
				
				<div class="shrink" on:click={handleShrunk}>
					&#10094;
				</div>

				<ShrunkPanel {active_data}/>
			</div>
		{/if}

		<ResizeObserver on:resize={(e) => setShrunk(e) } />

	</div>

{:else}
	<div class="wait">
		Loading.... <br>
		Please Wait...
	</div>
{/if}

<style>
	.wait{
		position: absolute;
		top: 50%;
		left: 50%;
		margin-top: -50px;
		margin-left: -50px;
	}

	.right-panel>.shrink{
		transform: rotate(-90deg);
	}

	.right-panel.shrunk>.shrink{
		transform: rotate(90deg);
	}

	.shrink{
		position:absolute;
		right:20px;
		top:12px;
		font-family: Arial, Helvetica, sans-serif;
		font-style: normal;
		color:#444;
		font-size:18pt;
		visibility: hidden;
		cursor: pointer;
	}

@media only screen and (max-width: 690px) {
    .shrink{
        visibility: visible;
    }
}
</style>
