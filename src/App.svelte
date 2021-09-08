<script>
	import LeafletMap from './Map.svelte'
	import {onMount} from 'svelte'
	import GeoJson from './Geojson.svelte';
	import GeoJsonBorder from './GeojsonBorder.svelte';
	import InfoPanel from './InfoPanel.svelte';
	import Legend from './Legend.svelte';

	const url_lots = "https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/data/BIP_FinalLots.geojson";
	const url_border = "https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/data/BIP_lines_4326.geojson";

	let active_data;

	let data = {
		bip:[],
		border:[],
		//parks:[]
	}

	onMount(async () => {
		const res = await fetch( url_lots );
		let data_lots = await res.json();
		data.bip = data_lots.features;

		const res2 = await fetch( url_border );
		let border_lots = await res2.json();
		data.border = border_lots.features;

		console.log(data);
	});

	//Handle Clicked Geojson Object, Point or Polygon. Returns active Polygon Object
	function handleMessage(e){
		 let active = e.detail.active;
		 let obj_id = active._path.id
		 obj_id = obj_id.split(" ")[0]

		active_data = data.bip.filter(function(feature){
			let blocklot = String(feature.properties.Block) + String(feature.properties.Lot);
			if( blocklot === obj_id ){
				return true
			}else{
				return false
			}
		})
	}
	
</script>

<svelte:head>
	<link rel="stylesheet" href="https://use.typekit.net/kjc8ltt.css">
</svelte:head>

{#if data.border.length > 0 }
	<div class="two-column">
		<div class="left-panel">
			<LeafletMap >
				<GeoJson on:message={handleMessage} geojson={data.bip} />
				<GeoJsonBorder geojson={data.border} />
				<Legend />
			</LeafletMap>
		</div>

		<div class="right-panel">
			<InfoPanel {active_data}/>
		</div>
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
</style>
