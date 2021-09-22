
<div class="legend">
    <div class="title"> Bushwick Inlet Park Lots</div>
    
    <div class="legend-item" >
        <div><hr></div>
        <div class="legend-text">Bushwick Inlet Park Boundary</div>
    </div>

    <div class="legend-item" >
        <div class="rect" style="background:var(--parkColor)"></div>
        <div class="legend-text">Owned and managed by<br> the NYC Parks Dept.</div>
    </div>

    <div class="legend-item" >
        <div class="rect" style="background:var(--stateColor)"></div>
        <div class="legend-text">Other Adjacent Waterfront Sites</div>
    </div>

</div>

<style>

    .legend-text{
        font-size: 10pt;
        font-weight: 400;
        margin-left: 8px;
        color:#444;
    }

    .title{
        font-size: 16pt;
        margin-bottom: 10px;
        font-weight: 700;
        color: #555;
    }

    hr{
        border: 2px dashed var(--borderOrange);
        stroke-dasharray: 3em 1em;
    }


    .legend-item{
        padding:5px;
        display: grid;
        grid-template-columns: 0.3fr 1fr;
    }

    .rect{
        width:100%;
        height:100%;
        stroke-dasharray: 2em;
        z-index:2001;
    }

</style>