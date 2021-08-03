
<div class="legend">
    <div class="title"> Bushwick Inlet Park Lots</div>
    
    <div class="legend-item" >
        <div><hr></div>
        <div class="legend-text">Bushwick Inlet Park Boundary</div>
    </div>

    <div class="legend-item" >
        <div class="rect" style="background:var(--parkColor)"></div>
        <div class="legend-text">Owned and managed by<br> the Parks Department</div>
    </div>

    <div class="legend-item" >
        <div class="rect" style="background:var(--stateColor)"></div>
        <div class="legend-text">Owned and managed by<br> New York State</div>
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

    .legend{
        position:absolute;
        bottom: 15px;
        left: 15px;
        background:rgba(255,255,255,0.75);
        width: 260px;
        height: 150px;
        z-index: 2000;
        padding:15px;
        line-height: 12pt;
        border-radius: 8px;
        border-style: solid;
        border-color: rgb(211, 211, 211);
        border-width: 2px;
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