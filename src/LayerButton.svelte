
<script>
    import { count } from "./store.js";
    import L from "leaflet";

    let map;
    count.subscribe(value => {
        map = value;
    });


    function reverseViz(){
        let legendstate = document.getElementsByClassName('legend')[0].style.visibility;
        if (legendstate === 'hidden'){
            document.getElementsByClassName('legend')[0].style.visibility = 'visible';
        } else {
            document.getElementsByClassName('legend')[0].style.visibility = 'hidden';
        }
        return false;
    }

    //Add button with function.
    L.easyButton('<i class="fa fa-ellipsis-v" aria-hidden="true"></i>', (btn,map)=>{
        reverseViz();
        event.preventDefault();
    }  

    ).addTo(map);


</script>
