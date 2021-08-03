
<script>
    import * as L from 'leaflet';
    import { count } from "./store.js";

    export let geojson;

    //countValue is map object stored in the store.js
    let map;
    count.subscribe(value => {
        map = value;
    });

    function style(feature) {
        return {
            color: "orange",
            fillOpacity: 0,
            weight: 2,
            opacity: 1,
        };
    }

    const layer = L.geoJSON(geojson,{
        style: style,
    }).addTo(map);

    // Assign a seperate ID for park and outside elements. 
    layer.eachLayer(function (polygon) {
            polygon._path.id = "Border"
            //console.log(polygon);
        });

</script>


<slot />