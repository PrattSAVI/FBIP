<script>

    function reverseViz(){

        /*  
        if (window.lastClick && new Date().getTime() - window.lastClick < 200) {
            window.lastClick = null;
            return;
        }
        window.lastClick = new Date().getTime();
        */

        let legendstate = document.getElementsByClassName('legend')[0].style.visibility;

        if ((legendstate === 'hidden') || ( legendstate.length === 0 )){
            document.getElementsByClassName('legend')[0].style.visibility = 'visible';
        } else {
            document.getElementsByClassName('legend')[0].style.visibility = 'hidden';
        }
        return false;
    }

    function handlelayer(){
        console.log('MOMO')
        reverseViz();
    }


</script>

<div class="homebutton" on:click={handlelayer}>
    <img alt="key" src="https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/img/key_icon.svg" >
</div>


<style>
    .homebutton{
        z-index: 800;
        height: 30px;
        width: 30px;
        position: absolute;
        top:130px;
        left:10px;
        background-color: white;
        text-align: center;
        border-radius: 4px;
        border:2px solid rgba(0,0,0,0.55);
        cursor: pointer;
    }

    img{
        width:22px;
        height:auto;
        margin:0 auto;
        margin-top: 9px;
    }
</style>