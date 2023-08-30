<script>
    import {onMount} from 'svelte'
    let wrapper;
    let degrees = 15000;
    let spinning = false;
    function rotateElement() {
        wrapper.style.transition = 'all 10s ease-out';
        wrapper.style.transform = `rotate(${degrees}deg)`;
        degrees+=10;
        console.log(degrees)
    }


    const startAnimationLoop = () => {
        rotateElement()
    }

</script>


<style>
    .wheel {
        border-radius: 100%;
        background-color: blue;
        min-width:600px;
        min-height:600px;
        animation:spin 1s ease-in-out;
        margin:2rem;
    }
</style>
    
<div class="wheel" bind:this={wrapper}>
    Test
</div>
<button on:click={startAnimationLoop}>Rotate</button>
