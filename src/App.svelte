<script>
	let name = 'puddle';
    let cansFed = 0;

    function feedHalfCan() {
        cansFed = cansFed + 0.5;
    }

    function feedFullCan() {
        cansFed = cansFed + 1;
    }

</script>

<h1 id='one'>{name} eats food</h1>

<button on:click={feedHalfCan}>half can</button>
<button on:click={feedFullCan}>full can</button>

<p>Food so far today: {cansFed}</p>
<p>Goal: 2.5</p>

<style>
    #one {
        color: blue;
    }
</style>