
<script>
    export let active_data;
    console.log( active_data );

</script>


<div class="right-content">

    {#if active_data}

        <p><span id='pane-title' >{active_data[0].properties['Text-Name']}</span></p>
        
        <div class="photo-loc"> <img alt="test" src="https://picsum.photos/250/250?random=1" /> </div>

        <div class="info-container">

            <p><span id='info-title' >{active_data[0].properties['Text-Acres']}</span></p>
            <p><span id='info-title' >{active_data[0].properties['Text-Address']}</span></p>
            <p><span id='info-title' >{active_data[0].properties['Text-Copy']}</span></p>

        </div>

    {:else}

        <div class="info-container">
            <p><span id='pane-title' >About the Map</span></p>
            <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Harum reiciendis, distinctio placeat inventore deleniti tenetur cupiditate mollitia, nemo asperiores beatae facilis ducimus aliquam libero saepe nesciunt excepturi rem pariatur cum?</p>
            <p>Partner Acknowledgments here. Don't Forget</p>

        </div>

    {/if}

</div>
