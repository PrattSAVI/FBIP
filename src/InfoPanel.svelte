
<script>
    import {beforeUpdate, afterUpdate} from "svelte";
    import Carousel from 'svelte-carousel'
    export let active_data;
 
    //List of all photos and BBLS
    let photos = [
        {site:"3022770000",photo:"1",credit:"Friends of Bushwick Inlet Park"},
        {site:"3022770000",photo:"2",credit:"Friends of Bushwick Inlet Park"},
        {site:"3022770000",photo:"3",credit:"Danny Lyon"},
        
        //50 Kent
        {site:"3022870000",photo:"1",credit:"NYC Dept of Parks & Recreation"},
        {site:"3022870000",photo:"2",credit:"NYC Dept of Parks & Recreation"},

        {site:"3022940001",photo:"1",credit:"Friends of Bushwick Inlet Park"},
        {site:"3022940001",photo:"2",credit:"Friends of Bushwick Inlet Park"},

        {site:"3023010060",photo:"1",credit:"Friends of Bushwick Inlet Park"},
        {site:"3023010060",photo:"2",credit:"Friends of Bushwick Inlet Park"},
        {site:"3023010060",photo:"3",credit:"Friends of Bushwick Inlet Park"},

        {site:"3023160001",photo:"1",credit:"Friends of Bushwick Inlet Park"},
        {site:"3023160001",photo:"2",credit:"NYS Dept of Parks, Recreation & Historic Preservation"},
        {site:"3023160001",photo:"3",credit:"Collection of Philip M. Goldstein"},

        {site:"3025900025",photo:"1",credit:"Greenpoint Monitor Museum"},
        {site:"3025900025",photo:"2",credit:"Greenpoint Monitor Museum"},
        {site:"3025900025",photo:"3",credit:"Greenpoint Monitor Museum"},

        {site:"3025900100",photo:"1",credit:"NYC Dept of Parks & Recreation"},
        {site:"3025900100",photo:"2",credit:"NYC Dept of Parks & Recreation"},
        {site:"3025900100",photo:"3",credit:"NYC Dept of Parks & Recreation"},

        {site:"3025900001",photo:"1",credit:"Google Maps"},
        {site:"3025900001",photo:"2",credit:"Google Maps"},
        {site:"3025900001",photo:"3",credit:"FEMA"},
    ]

    let active_photos = [];

    //Remove credits if they are repeting and convert the list to "," seperated text
    function getCredits(data){
        let a = []
        data.forEach(function(d){
            a.push(d.credit)
        })
        a = [...new Set(a)]; // Remove Duplicates
        return a.join(', ');
    }

    //filter photos & scrollto top. 
    afterUpdate(() => {
        //Filter photos to active data
		if (active_data){

            //Filter photos by active data
            active_photos = photos.filter(function(photo){
                return photo.site === active_data[0].properties.BBL;
            })


        //Scroll to top on active data change. 
        let element = document.getElementsByClassName("right-panel")[0];
        element.scroll({
            top:0,
            behavior:'auto'
        });
        
        //If the scroll did not work, try again. 
        setTimeout(function(){ 
            if(element.scrollTop !== 0){
                element.scroll({
                    top:0,
                    behavior:'auto'
                });
            }
         }, 500);
        }
	});


</script>


<div class="right-content">

    {#if active_data}

        <div class="info-title">
            <span id='pane-title' >{active_data[0].properties['Text-Name']}</span>
        </div>
        

        {#key active_photos}
            <div class="photo-container">
                
                <Carousel
                    let:showPrevPage
                    let:showNextPage
                >

                    <div slot="prev" on:click={showPrevPage} class="custom-arrow custom-arrow-prev">
                        <i>&#10094;<i />
                    </div>

                    {#each active_photos as photo }  
                        <img class="container-photos" alt="test" src= "https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/img/{photo.site}/{photo.photo}.jpg" />  
                    {/each}

                    <div slot="next" on:click={showNextPage} class="custom-arrow custom-arrow-next">
                        <i>&#10095;<i />
                    </div>

                </Carousel>
            </div>
        
        {/key}


        <div class="info-container">

            <p><span id='info-title' >{active_data[0].properties['Text-Acres']}</span></p>
            <p><span id='info-title' >{active_data[0].properties['Text-Address']}</span></p>

            {#if active_data[0].properties['Text-Copy']}
                <p><span id='info-title' >{@html active_data[0].properties['Text-Copy']}</span></p>
            {:else}
                <p><strong>Status: </strong><span id='info-title' >{@html active_data[0].properties['Text_History']}</span></p>
                <p><strong>History: </strong> <span id='info-title' >{@html active_data[0].properties['Text_Status']}</span></p>
            {/if}

            {#if active_data[0].properties['Text_Web']}
                <p><strong>Website: </strong><span id='info-title' ><a href={active_data[0].properties['Text_Web']} target="_blank">{active_data[0].properties['Text_Web']}</a></span></p>
            {/if}

            {#if active_photos}
                <p class='photo-credit'>Photo Credits: {getCredits(active_photos)}</p>
            {/if}

        </div>

    {:else}

        <div class="info-title">
            <span id='pane-title' >BIP Parcel Map</span>
        </div>

        <div class="info-container">
            <p>Bushwick Inlet Park is a mosaic public park project. Its multiple sections are in various phases of development. This map aims to help simplify this picture. Click or tap on a section within the park’s borders or adjacent spaces to see images, brief histories and the current development status of each space.
            <br><br>This project is a collaboration between Pratt Institute’s <a href="https://commons.pratt.edu/savi/" target="_blank">Spatial Analysis & Visualization Initiative (SAVI)</a> and Friends of Bushwick Inlet Park. Support for this project has been provided by the 
            <span style="color:var(--parkColor);font-weight:bold">Brooklyn Borough President,</span> <span style="color:var(--parkColor);font-weight:bold">City Parks Foundation</span> and the 
            <span style="color:var(--parkColor);font-weight:bold">NYC Green Relief & Recovery Fund</span>.
            </p>
        </div>

    {/if}

</div>






<style>

.custom-arrow{
    font-family: Arial, Helvetica, sans-serif;
    font-style: normal;
    color:#222;
    font-size:18pt;
    font-weight: 900;
    width:30px;
    height:100%;
    position:absolute;
    z-index:3;
    background:rgba(255,255,255,0.15)!important;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
}

.custom-arrow.custom-arrow-next{
    right:0;
}
	
.custom-arrow.custom-arrow-prev{
    left:0
}

i{
    font-style: normal!important;
}

</style>
