<script>
    // Nested components
    import Nested from "./Nested.svelte";

    // variable
    let name = "Amine Elkhalidy";

    // HTML tags
    let string = `this string contains some <strong>HTML!!!</strong>`;

    let count = 0;
    // reactive declarations
    $: doubled = count * 2;

    // reactive statements
    $: console.log(`the count is ${count}`);
    function handleClick(){
        count += 1;
    }

    // arrays and objects
    let numbers = [1, 2, 3, 4];

	function addNumber() {
		numbers = [...numbers, numbers.length + 1]
	}
    $: sum = numbers.reduce((total, currentNumber) => total + currentNumber, 0);

    // each block
    const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'];
	let selected = colors[0];
</script>

<h1>Hello World!</h1>
<h2>I am {name.toUpperCase()}</h2>

<!-- Component Props -->
<Nested answer='This is the answer property' />
<Nested />

<p>{@html string}</p>

<button on:click={handleClick}>
    Clicked {count} {count === 1 ? 'time' : 'times'}
</button>

<!-- if, else if and else -->
{#if count > 10}
<p>{count} is greater than 10</p>
{:else if count < 5}
<p>{count} is less than 5</p>
{:else}
<p>{count} is between 5 and 10</p>

{/if}


<p>{count} double is {doubled}</p>

<p>{numbers.join(' + ')} = {sum}</p>
<button on:click={addNumber}>
	Add a number
</button>

<hr />
<h1 style="color: {selected}">Pick a colour</h1>
{#each colors as color}
<button
		aria-current={selected === color}
		aria-label={color}
		style="background: {color}"
		on:click={() => selected = color}
	>{color}</button>
{/each}

<style>
   h1 {
		transition: color 0.2s;
	}

	div {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-gap: 5px;
		max-width: 400px;
	}

	button {
		aspect-ratio: 1;
		border-radius: 50%;
		background: var(--color, #fff);
		transform: translate(-2px,-2px);
		filter: drop-shadow(2px 2px 3px rgba(0,0,0,0.2));
		transition: all 0.1s;
	}

	button[aria-current="true"] {
		transform: none;
		filter: none;
		box-shadow: inset 3px 3px 4px rgba(0,0,0,0.2);
	}
</style>