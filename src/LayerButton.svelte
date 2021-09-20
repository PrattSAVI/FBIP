
<script>
    import { count } from "./store.js";
    import L from "leaflet";

    let map;
    count.subscribe(value => {
        map = value;
    });

    let momo = 0;
    let layer = L.easyButton('<i class="fa fa-bars" aria-hidden="true"></i>', function(btn, map){
        
        momo = momo+1;
        //This button is firing twice. I am ignoring the 2.clicks. 
        if (momo % 2 === 1){
            let legendstate = document.getElementsByClassName('legend')[0].style.visibility;
            console.log( legendstate);

            if (legendstate === 'hidden'){
                document.getElementsByClassName('legend')[0].style.visibility = 'visible';
            } else {
                document.getElementsByClassName('legend')[0].style.visibility = 'hidden';
            }
        }
    });
    
    layer.addTo(map);

</script>
