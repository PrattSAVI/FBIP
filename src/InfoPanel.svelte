
<script>
    export let active_data;
    console.log( active_data );

</script>


<div class="right-content">

    
    {#if active_data}
        
        <div class="photo-loc"> <img alt="test" src="https://picsum.photos/150/150?random=1" /> </div>

        {#if active_data[0].properties.OwnerName}

            <div class="info-container">
                <p><span id='info-title' >{active_data[0].properties.OwnerName}</span></p>
                <p><span id='info-title' >{active_data[0].properties.Address}</span></p>
            </div>
        {/if}


    {:else}

        <div class="info-container">
            <p><strong>About this Map</strong></p>
            <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Harum reiciendis, distinctio placeat inventore deleniti tenetur cupiditate mollitia, nemo asperiores beatae facilis ducimus aliquam libero saepe nesciunt excepturi rem pariatur cum?</p>
        </div>

    {/if}





</div>

<style>
    .right-content{
        padding: var(--hh) 15px 10px 15px;
    }

    .photo-loc{
        width:150px;
        height:150px;
        background: #888;
    }

</style>