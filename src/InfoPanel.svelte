
<script>
    import {afterUpdate} from "svelte";
    export let active_data;

    //List of all photos and BBLS
    let photos = [
        {site:"3022770000",photo:"1"},
        {site:"3022770000",photo:"2"},
        {site:"3022770000",photo:"3"},
        {site:"3022770000",photo:"4"},
        {site:"3022870000",photo:"1"},
        {site:"3022870000",photo:"2"},

        {site:"3022940001",photo:"1"},
        {site:"3022940001",photo:"2"},

        {site:"3023010060",photo:"1"},
        {site:"3023010060",photo:"2"},

        {site:"3023160001",photo:"1"},
        {site:"3023160001",photo:"2"},
        {site:"3023160001",photo:"3"},

        {site:"3025900025",photo:"1"},
        {site:"3025900025",photo:"2"},
        {site:"3025900025",photo:"3"},
        {site:"3025900025",photo:"4"},

        {site:"3025900100",photo:"1"},
        {site:"3025900100",photo:"2"},
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

            {#each active_photos as photo }
                <div class="photo-loc"> 
                    <img alt="test" src= "https://raw.githubusercontent.com/PrattSAVI/FBIP/main/public/img/{photo.site}/{photo.photo}.jpg" /> 
                </div>
            {/each}

        </div>

        <div class="info-container">

            <p><span id='info-title' >{active_data[0].properties['Text-Acres']}</span></p>
            <p><span id='info-title' >{active_data[0].properties['Text-Address']}</span></p>
            <p><span id='info-title' >{active_data[0].properties['Text-Copy']}</span></p>

        </div>

    {:else}

        <div class="info-title">
            <span id='pane-title' >About the Map</span>
        </div>

        <div class="info-container">
            
            <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Harum reiciendis, distinctio placeat inventore deleniti tenetur cupiditate mollitia, nemo asperiores beatae facilis ducimus aliquam libero saepe nesciunt excepturi rem pariatur cum?</p>
            <p>Partner Acknowledgments here. Don't Forget</p>

        </div>

    {/if}

</div>

<style>
    .info-title{
        padding-left:10px;
        padding-right: 10px;
        margin-top: 25px;
        padding-bottom: 25px;
    }
</style>
