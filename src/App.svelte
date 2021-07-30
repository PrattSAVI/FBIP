<script>
	import LeafletMap from './Map.svelte'
	import Header from './Header.svelte'
	import {onMount} from 'svelte'
	import GeoJson from './Geojson.svelte';
	import InfoPanel from './InfoPanel.svelte';

	const url_lots = "/data/BIP_Lots_se_84.geojson";

	let data_lots;
	let active_data;

	onMount(async () => {
		const res = await fetch( url_lots );
		data_lots = await res.json();
		data_lots = data_lots.features;

		console.log(data_lots);

	});

	//Handle Clicked Geojson Object, Point or Polygon. Returns active Polygon Object
	function handleMessage(e){
		 let active = e.detail.active;
		 let obj_id = active._path.id
		 obj_id = obj_id.split(" ")[0]

		active_data = data_lots.filter(function(feature){
			let blocklot = String(feature.properties.Block) + String(feature.properties.Lot);
			if( blocklot === obj_id ){
				return true
			}else{
				return false
			}
		})
	}
	
</script>

<Header />
{#if data_lots}

	<div class="two-column">
		<div class="left-panel">
			<LeafletMap >
				<GeoJson on:message={handleMessage} geojson={data_lots} />
			</LeafletMap>
		</div>

		<div class="right-panel">
			<InfoPanel {active_data}/>
		</div>
	</div>
{/if}


