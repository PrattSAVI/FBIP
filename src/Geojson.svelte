
<script>
    import * as L from 'leaflet';
    import { count } from "./store.js";

    import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

    export let geojson;
    //console.log(geojson)

    //countValue is map object stored in the store.js
    let map;
    count.subscribe(value => {
        map = value;
    });

    //Zoom to active polygon and write id to store.
    function activePolygon(e){

        map.setView( e.target.getBounds().getCenter() ,17)

        //Set an active class to clicked Element
        let active = [...document.getElementsByClassName("active")];
        if (active.length > 0){ //If an element is selected
            active.forEach( function(feature){
                feature.className.baseVal = 'leaflet-interactive'; //Set it back to leaflet
            })
        }

        //Bring all polygons, (layer) back so that the border is visible
        layer.bringToBack();

        e.target._path.className.baseVal = e.target._path.className.baseVal + " active";
        e.target.bringToFront()
        
        //Send active ID out
        dispatch('message', {
			active: e.target
		}); 
    }

    function getColor(d) {
        return d === "State" ? "var(--stateColor)" :
            d === "Parks"  ? "var(--parkColor)" :
            d === ""  ? "FFFFFF" :
                        '#FFFFFF';
    }
    function LineColor(d) {
        return d === "State" ? "white" :
            d === "Parks"  ? "white" :
            d === ""  ? "black" :
                        '#000000';
    }
    function lineWeight(d) {
        return d === "State" ? 0.8 :
            d === "Parks"  ? 0.8 :
            d === ""  ? .5:
                        .5;
    }

    // 1.BIP Lot STYLE
    function style(feature) {
        return {
            fillColor: getColor(feature.properties.Owner),
            color: LineColor(feature.properties.Owner),
            fillOpacity: 0.9, //getFill(feature.properties.Owner),
            weight: lineWeight(feature.properties.Owner),
            opacity: 0.9,
        };
    }

    function onEachFeature(feature, layer) {
        //Only bind popup if BIP Column is not empty
        if( feature.properties.BIP ){
            layer.openTooltip();
            layer.on({
                click:activePolygon,
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

            //Add Labels
            if( polygon.feature.properties.BIP ){
                polygon.bindTooltip(polygon.feature.properties['Text-Name'],{
                    permanent:true,
                    direction: 'center',
                    offset: [-40, -20]
                } ).openTooltip();
            }
    });

    //Hide tooltips based on zoom level. Currently This is set to 17
    map.on('zoomend', function(e){
        var zoomLevel = map.getZoom();
        if (zoomLevel < 17 ){
            [].forEach.call(document.querySelectorAll('.leaflet-tooltip'), function (el) {
                el.style.visibility = 'hidden';
            });
        }else{
            [].forEach.call(document.querySelectorAll('.leaflet-tooltip'), function (el) {
                el.style.visibility = 'visible';
            });
        }
    });


</script>


<slot />