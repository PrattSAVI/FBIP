<script>
	import LeafletMap from './Map.svelte'
	//import Header from './Header.svelte'
	import {onMount} from 'svelte'
	import GeoJson from './Geojson.svelte';
	import GeoJsonBorder from './GeojsonBorder.svelte';
	import InfoPanel from './InfoPanel.svelte';
	import GeojsonParks from './GeojsonParks.svelte';

	const url_lots = "/data/BIP_FinalLots.geojson";
	const url_border = "/data/BIP_boundary_4326.geojson";
	const url_parks = "data/FBIP_other_parks_4326.geojson"

	let active_data;

	let data = {
		bip:[],
		border:[],
		parks:[]
	}

	onMount(async () => {
		const res = await fetch( url_lots );
		let data_lots = await res.json();
		data.bip = data_lots.features;

		const res2 = await fetch( url_border );
		let border_lots = await res2.json();
		data.border = border_lots.features;

		const res3 = await fetch( url_parks );
		let park_lots = await res3.json();
		data.parks = park_lots.features;

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


{#if data.parks.length > 0 }
	<div class="two-column">
		<div class="left-panel">
			<LeafletMap >
				<GeoJsonBorder geojson={data.border} />
				<GeojsonParks geojson={data.parks} />
				<GeoJson on:message={handleMessage} geojson={data.bip} />


			</LeafletMap>
		</div>

		<div class="right-panel">
			<InfoPanel {active_data}/>
		</div>
	</div>
{/if}


