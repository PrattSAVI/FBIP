
<script>
    import * as L from 'leaflet';
    import { count } from "./store.js";

    import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

    let map_blue = "var(--blue)";
    let map_green = "var(--green)";
   
    export let geojson;
    console.log(geojson)

    //countValue is map object stored in the store.js
    let map;
    count.subscribe(value => {
        map = value;
    });

    //Zoom to active polygon and write id to store.
    function activePolygon(e){
        map.setView( e.target.getBounds().getCenter() ,18)
        dispatch('message', {
			active: e.target
		}); 
    }

    //Sara's styling functions. 
    function getColor(d) {
        return d === "State" ? "var(--stateColor)" :
            d === "Parks"  ? "var(--parkColor)" :
            d === ""  ? "FFFFFF" :
                        '#FFFFFF';
    }
    function LineColor(d) {
        return d === "State" ? "#4f8f0a" :
            d === "Parks"  ? "#1a5b91" :
            d === ""  ? "black" :
                        '#000000';
    }
    function getFill(d) {
        return d === "State" ? "0.8" :
            d === "Parks"  ? "0.8" :
            d === ""  ? "0.4" :
                        "0.4";
    }
    function lineWeight(d) {
        return d === "State" ? 3 :
            d === "Parks"  ? 3 :
            d === ""  ? .5:
                        .5;
    }

    // 1.BIP Lot STYLE
    function style(feature) {
        return {
            fillColor: getColor(feature.properties.Owner),
            color: LineColor(feature.properties.Owner),
            fillOpacity: getFill(feature.properties.Owner),
            weight: lineWeight(feature.properties.Owner),
            opacity: 1,
        };
    }

    function onEachFeature(feature, layer) {
        //Only bind popup if BIP Column is not empty
        if( feature.properties.BIP ){
            var popupContent = `${feature.properties.OwnerName}`;
            layer.bindPopup(popupContent);
            layer.on({
                click:activePolygon,
                mouseover: e => {layer.openPopup()},
                mouseout: e => {layer.closePopup()}
            }) 
        }
    };

    const layer = L.geoJSON(geojson,{
        style: style,
        onEachFeature: onEachFeature,
    }).addTo(map);

    // Assign a seperate ID for park and outside elements. 
    layer.eachLayer(function (polygon) {
            let filler = polygon._path.attributes.fill.value;
            if (filler === "#FFFFFF"){
                polygon._path.id = String(polygon.feature.properties.Block) + String(polygon.feature.properties.Lot) + " outside"
            }else{
                polygon._path.id = String(polygon.feature.properties.Block) + String(polygon.feature.properties.Lot) + " bip"
            }
        });

</script>


<slot />