<script>
    let inputValue = ''
    let players = [];
    let isMenuVisible = false;
    let faultyOption = false;
    let selectedRank = 'Rank'
    const ranks = ['SSL','GC3','GC2','GC1','C3','C2','C1','Diamond','Platinum','Gold','Silver','BronzeLMAO']

    const handlePress = (event) => {
        if(ranks.includes(selectedRank) && inputValue.length >= 4) {
            faultyOption = false;
            players = [...players, {'name': inputValue, 'rank':selectedRank}]
            inputValue = ''
            selectedRank = 'Rank'
            return;
        }
        faultyOption = true;
        if(faultyOption) {
            setInterval(() => {
                faultyOption = false;
            },5000);
        }
    }
    const toggleMenu = () => {
        isMenuVisible = !isMenuVisible;
    }
    const setRank = (param) => {
        selectedRank = param;
        toggleMenu();
    }

</script>
<div class="player-screen">
    <div class="header-page">
        <input type="text" bind:value={inputValue}/>
        <div class="dropdown">
            <button on:click={toggleMenu}>{selectedRank || 'Rank'}</button>
            <button on:click={handlePress}>Add Player</button>
            <ul class="menu" class:selected={isMenuVisible}>
                {#each ranks as rank} 
                <li><button on:click={() => {setRank(rank)}}>^ {rank}</button></li>
                {/each}
            </ul>
        </div>
        </div>
        {#if players.length > 0}
        <div class="players">
            {#each players as player}
            <p class="individual-player">{player.name} {player.rank}</p>
            {/each}
        </div>
        {/if}
        <p style="color: red" class="ErrorMessage" class:selected={faultyOption}> Please select rank first</p>
    </div>
<style>
    .individual-player {
        background:rgba(17, 29, 65, 0.694);
        padding:.4rem;
        border-radius:5px;
        margin:1rem;

    }
    .player-screen {
        margin:1rem;
        display:flex;
        flex-direction:column;
    }
    .players {
        border-radius: 10px;
        background:rgba(1, 1, 1, 0.464);
        padding:0.25em;
        margin:1em 0em;
        
    }
    * {
        box-sizing: border-box;
    }
    .ErrorMessage {
        display:none;
        background:rgba(1,1,1,.5);
        padding:1.25rem;
        border-radius:15px;
        box-shadow:0px 0px 8px 2px rgb(195, 59, 96);
        width:100%;
        z-index:1;
    }

    .header-page {
        max-height:80px;
        background:gray;
        padding:1rem;
        border-radius: 5px;
        display:grid;
        grid-template-columns: 1fr 1fr;
    }
    .dropdown {
        min-width:15em;
        position:relative;
    }
    .menu {
        background: rgb(34, 30, 38);
        display:none;
        list-style:none;
        position:absolute;
        left:20px;
        top:30px;
        padding:0 2rem;
        border-radius:15px;
    }
    .menu li {
        cursor:pointer;
        padding:.25rem;
        margin:.75rem 0;
        display:flex;
        align-items: center;
        justify-content: center;
        border-radius:5px;
        box-shadow:0px 0px 3.5px 3.5px rgb(81, 3, 81);
        background-color: black;
        transition:background-color .25s;
    }
    .menu li:hover {
        background-color: rgb(22, 22, 49);
    }
    .menu button {
        width:100%;
        background:transparent;
        border:none;
    }
    .menu button:hover {
        box-shadow: 0px 0px 0px 0px white;
    }
    .selected {
        display:block;
    }
</style>