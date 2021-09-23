
<div class="legend">
    <div class="title"> Bushwick Inlet Park Lots</div>
    
    <div class="legend-item" >
        <div><hr></div>
        <div class="legend-text">Bushwick Inlet Park Boundary</div>
    </div>

    <div class="legend-item" >
        <div class="rect" style="background:var(--parkColor)"></div>
        <div class="legend-text">Owned and managed by the <br>NYC Parks Dept.</div>
    </div>

    <div class="legend-item" >
        <div class="rect" style="background:var(--stateColor)"></div>
        <div class="legend-text">Other Adjacent<br>Waterfront Sites</div>
    </div>

</div>

<style>

    .legend {
        position:absolute;
        bottom:18px;
        left:15px;
        font-size: 8pt;
        width: 230px;
        height: 100px;
        z-index: 2000;
        padding: 8px;
        line-height: 0.8rem;
        border-radius: 8px;
        border-style: solid;
        border-color: rgb(211, 211, 211);
        background-color: white;
        border-width: 2px;
        pointer-events: none;
    }

    .legend-text{
        font-size: 9pt;
        font-weight: 400;
        margin-left: 8px;
        color:#444;
    }

    .title{
        font-size: 11pt;
        margin-bottom: 6px;
        font-weight: 700;
        color: #555;
    }

    hr{
        border: 2px dashed var(--borderOrange);
        stroke-dasharray: 3em 1em;
    }

    .legend-item{
        padding:3px;
        display: grid;
        grid-template-columns: 0.2fr 1fr;
    }

    .rect{
        width:100%;
        height:100%;
        stroke-dasharray: 2em;
        z-index:2001;
    }

</style>