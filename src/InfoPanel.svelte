
<script>
    import {afterUpdate} from "svelte";
    import Carousel from 'svelte-carousel'
    export let active_data;

    //List of all photos and BBLS
    let photos = [
        {site:"3022770000",photo:"1",credit:"Friends of Bushwick Inlet Park"},
        {site:"3022770000",photo:"2",credit:"Friends of Bushwick Inlet Park"},
        {site:"3022770000",photo:"3",credit:"Danny Lyon"},
        
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

        {site:"3025900100",photo:"1",credit:"Motiva"},
        {site:"3025900100",photo:"2",credit:"Motiva"},
        {site:"3025900100",photo:"3",credit:"Motiva"},

        {site:"3025900001",photo:"1",credit:"Google Maps"},
        {site:"3025900001",photo:"2",credit:"Google Maps"},
        {site:"3025900001",photo:"3",credit:"FEMA"},
    ]

    let active_photos = [];

    afterUpdate(() => {
        //Filter photos to active data
		if (active_data){
            active_photos = photos.filter(function(photo){
                //console.log( "BBL: " + active_data[0].properties.BBL )
                //console.log( "Site: " + photo.site )
                return photo.site === active_data[0].properties.BBL
            })
        }
	});


</script>


<div class="right-content">

    {#if active_data}

        <div class="info-title">
            <span id='pane-title' >{active_data[0].properties['Text-Name']}</span>
        </div>
        
        <div class="photo-container">

            <Carousel
                let:showPrevPage
                let:showNextPage
                >
                    <div slot="prev" on:click={showPrevPage} class="custom-arrow custom-arrow-prev"><i /></div>
                        {#each active_photos as photo }  
                        <img alt="test" src= "https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/img/{photo.site}/{photo.photo}.jpg" />  
                    {/each}
                    <div slot="next" on:click={showNextPage} class="custom-arrow custom-arrow-next"><i /></div>
                </Carousel>

        </div>

        <div class="info-container">

            <p><span id='info-title' >{active_data[0].properties['Text-Acres']}</span></p>
            <p><span id='info-title' >{active_data[0].properties['Text-Address']}</span></p>
            <p><span id='info-title' >{active_data[0].properties['Text-Copy']}</span></p>
            <br>
            <p><span class='photo-credit'>Photo Credits:</span></p> 
            {#each active_photos as photo } 
                   
                <span class='photo-credit'>{photo.credit}</span><br>

            {/each}

        </div>

    {:else}

        <div class="info-title">
            <span id='pane-title' >About the Map</span>
        </div>

        <div class="info-container">
            <p>Bushwick Inlet Park is a mosaic public park project. Its multiple sections are in various phases of development. This map aims to help simplify this picture. Click or tap on a section within the park’s borders or adjacent spaces to see images, brief histories and the current development status of each space.
            <br><br>This project is a collaboration between Pratt Institute’s <a href="https://commons.pratt.edu/savi/" target="_blank">Spatial Analysis & Visualization Initiative (SAVI)</a> and Friends of Bushwick Inlet Park. Support for this project has been provided by the <span style="color:var(--parkColor);font-weight:bold">City Parks Foundation</span> and the <span style="color:var(--parkColor);font-weight:bold">NYC Green Relief & Recovery Fund.</span>.
            </p>
        </div>

    {/if}

</div>
