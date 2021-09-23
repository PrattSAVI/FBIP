
<script>
    import { count } from "./store.js";
    import L from "leaflet";

    let map;
    count.subscribe(value => {
        map = value;
    });


    function reverseViz(){

        
        if (window.lastClick && new Date().getTime() - window.lastClick < 200) {
            window.lastClick = null;
            return;
        }
        window.lastClick = new Date().getTime();
        

        let legendstate = document.getElementsByClassName('legend')[0].style.visibility;
        
        if ((legendstate === 'hidden') || ( legendstate.length === 0 )){
            document.getElementsByClassName('legend')[0].style.visibility = 'visible';
        } else {
            document.getElementsByClassName('legend')[0].style.visibility = 'hidden';
        }
        return false;
    }

    //Add button with function.
    L.easyButton('<img class="symbol-key" src="https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/img/key_icon.svg" >', (btn,map)=>{
        reverseViz();
        event.preventDefault();
    }  

    ).addTo(map);


</script>

