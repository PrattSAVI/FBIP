
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

    .legend {
        position:absolute;
        bottom:15px;
        left:15px;
        font-size: 10pt;
        width: 260px;
        height: 130px;
        z-index: 2000;
        padding: 15px;
        line-height: 10pt;
        border-radius: 8px;
        border-style: solid;
        border-color: rgb(211, 211, 211);
        background-color: white;
        border-width: 2px;
        pointer-events: none;
    }

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