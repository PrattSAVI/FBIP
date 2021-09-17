
<script>
    export let active_data;

</script>


<div class="right-content">

    {#if active_data}

        <div class="info-title">
            <span id='pane-title' >{active_data[0].properties['Text-Name']}</span>
        </div>

    {:else}

        <div class="info-title">
            <span id='pane-title' >About the Map</span>
        </div>

    {/if}

</div>

