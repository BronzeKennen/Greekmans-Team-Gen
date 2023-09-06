<script>
    import {playersStore} from '../playerStore'
    import Players from './Players.svelte';
    let wheels = [];
    let players = [];
    let perzent = 100;
    let wheel;
    playersStore.subscribe(async (val) => {
        await Promise.resolve(players = val);
        await Promise.resolve(setWheel(players));
    });
    let wrapper;
    let spinning = false;
    function rotateElement() {
        let degrees = Math.random() * 10000;
        wrapper.style.transition = 'all 10s ease-out';
        wrapper.style.transform = `rotate(${degrees}deg)`;
        degrees+=10;
    }
    function setWheel(players) {
        if(players.length > 4) perzent -= 10;
        if(wheel) {
            wheels.push(wheel);
            wheels.forEach((wheel) => {
                console.log(wheel);
                wheel.style.transform = `rotate(calc(${360 / players.length}deg * var(--i)))`
                wheel.style.clipPath = `polygon(0 0, ${perzent}% 0, 100% 100%, 0% ${perzent}%)`
            })
            return wheels;
        }
    }


    const startAnimationLoop = () => {
        rotateElement()
    }

</script>

<style>
    .wheel {
        margin:1rem;
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
    }
    .player-info-in {
        position:absolute;
        width:50%;
        height:50%;
        transform-origin: bottom right;
        transform: rotate(calc(70deg * var(--i)));
        background:var(--clr);
        clip-path: polygon(0 0, 74% 0, 100% 100%, 0% 74%);
        display:flex;
        justify-content: center;
        align-items: center;
        user-select: none;
        cursor:pointer;
    }
    .player-info-in span {
        position:relative;
        transform: rotate(calc(140deg));
        font-size:1.5rem;
        font-weight: 700;
    }
    .arrow {
        position:absolute;
        z-index:1;
        top:45.5%;
        left:46%;
        width:50px;
        height:50px;
        transform: rotate(90deg);
    }
</style>


<div class="wheel">
    <img src="./arrow2.png" class="arrow" alt='arrow'>
    <div class="player-triangle" bind:this={wrapper}>
    {#each players as player,index}
        <div id="wheelItem"class="player-info-in" style="--i:{index};--clr:#{(index+1)*100};" bind:this={wheel}>
            <span>{player.name}</span>
        </div>
    {/each}
    </div>
</div>
<button on:click={startAnimationLoop}>Rotate</button>


