
<script>
    import * as L from 'leaflet';
    import { count } from "./store.js";
    import {afterUpdate} from "svelte";

    export let geojson;

    //countValue is map object stored in the store.js
    let map;
    count.subscribe(value => {
        map = value;
    });

    //White Line Behind the dashed Border
    function styleBehind(feature) {
        return {
            color: "white",
            weight: 5,
        };
    }

    const layerBehind = L.geoJSON(geojson,{
        style: styleBehind,
    }).addTo(map);

    //Dashed Orange Line
    function style(feature) {
        return {
            color: "var(--borderOrange)",
            weight: 4,
            dashArray: '5, 3', 
            lineCap: 'butt',
        };
    }

    const layer = L.geoJSON(geojson,{
        style: style,
    }).addTo(map);

    
    // Assign a seperate ID for park and outside elements. 
    layer.eachLayer(function (polygon) {
            polygon._path.id = "Border"            
        });

    layer.eachLayer(function (polygon) {
        polygon._path.id = "BorderBehind"
        
    });

    //Add Label to the whole park
    // Add Point
    var newMarker = new L.circle( L.latLng(40.723,-73.961) ,{
        stroke:false,
        opacity:0,
        fillOpacity:0
    } ).addTo(map);

    //Add label
    newMarker.bindTooltip( "Bushwick Inlet Park",{
        permanent:true,
        direction: 'center',
    }).openTooltip();

    afterUpdate(() => {
        //Filter photos to active data
        setTimeout( function(){
           
            [].forEach.call(document.querySelectorAll('.leaflet-tooltip'), function (el) {
                if( el.innerHTML === "Bushwick Inlet Park" ){
                    el.style.visibility = 'hidden';
                }else{
                    el.style.visibility = 'visible';
                }
            });

        },500)
	});
  
	
    
</script>


<slot />