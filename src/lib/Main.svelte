<script>
    let inputValue = ''
    let values = []
    let isMenuVisible = false;

    const handlePress = (event) => {
        if(event.key === 'Enter') {
            values = [...values, inputValue]
            inputValue = ''
        }
    }
    const toggleMenu = () => {
        isMenuVisible = !isMenuVisible;
    }

</script>

<div class="header-page">
    <input type="text" bind:value={inputValue} on:keydown={handlePress}/>
    <div class="dropdown">
        <button on:click={toggleMenu}>Rank</button>
        <ul class="menu" class:selected={isMenuVisible}>
            <li >^ SLL</li>
            <li>^ GC3</li>
            <li>^ GC2</li>
            <li>^ GC1</li>
            <li>^ C3</li>
            <li>^ C2</li>
            <li>^ C1</li>
            <li>^ Diamond</li>
            <li>^ Plat</li>
            <li>^ Gold</li>
            <li>^ Silver</li>
            <li>^ BronzeLMAO</li>
        </ul>
    </div>
    {#each values as value}
        <p>{value}</p>
    {/each}
</div>

<style>
    .header-page {
        background:gray;
        margin:1rem;
        border-radius: 5px;
        display:grid;
        grid-template-columns: 1fr 1fr;
    }
    .dropdown {
        min-width:15em;
        position:relative;
    }
    .menu {
        background: rgb(46, 31, 58);
        display:none;
        list-style:none;
        position:absolute;
        left:20px;
        top:30px;
        padding:0 2rem;
    }
    .menu li {
        padding:.25rem;
        display:flex;
        align-items: center;
        justify-content: center;
    }
    .selected {
        display:block;
    }
</style>