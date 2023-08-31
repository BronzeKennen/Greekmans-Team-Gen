<script>
    import {playersStore} from '../playerStore'

    let players = [];
    playersStore.subscribe((val) => players = val);
    let wrapper;
    let degrees = 25000;
    let spinning = false;
    function rotateElement() {
        wrapper.style.transition = 'all 10s ease-out';
        wrapper.style.transform = `rotate(${degrees}deg)`;
        degrees+=10;
    }


    const startAnimationLoop = () => {
        rotateElement()
    }

</script>

<style>
    .wheel {
        position:relative;
        width:600px;
        height:600px;
        display:flex;
        justify-content: center;
        align-items: center;
        animation:spin 1s ease-in-out;
    }
    .player-triangle {
        position:absolute;
        top:0;
        left:0;
        width:100%;
        height:100%;
        background:#0f245e7b;
        border-radius: 100%;
        overflow:hidden;
        box-shadow: 0 0  0 5px #333,
        0 0 0 15px #fff,
        0 0 0 18px #111;
        border:1px red solid;
    }
    .player-info-in {
        position:absolute;
        width:50%;
        height:50%;
        transform-origin: bottom right;
        border:1px yellow solid;
        transform: rotate(calc(72deg * var(--i)));
        background:var(--clr);
        clip-path: polygon(0 0, 85% 0, 100% 100%, 1% 85%);
        display:flex;
        justify-content: center;
        align-items: center;
        user-select: none;
        cursor:pointer;
    }
    .player-info-in span {
        position:relative;
        transform: rotate(calc(140deg));
        font-size:2rem;
    }
</style>


<div class="wheel" bind:this={wrapper}>
    <div class="player-triangle">
    {#each players as player,index}
        <div class="player-info-in" style="--i:{index};--clr:#{(index+1)*100};">
            <span>{player.name}</span>
        </div>
    {/each}
    </div>
</div>
<button on:click={startAnimationLoop}>Rotate</button>


