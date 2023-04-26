<script>
  $: data = [...Array(10)].map(_=>Math.ceil(Math.random()*40));
  $: current = 0;
  $: lowest = data[current];
  $: sorted = current === data.length - 1 ? true : false;

  const selectionSort = () => {
    let firstIndex = current;

    for (var j = current + 1; j < data.length; j++) {
      if (data[j] < data[firstIndex]) {
        firstIndex = j;
      }
    }
    if (!sorted) {
      let temp = data[firstIndex];
      data[firstIndex] = data[current];
      data[current] = temp;
      current++;
      lowest = temp;
    }
  };

  const reset =()=>{
    data = [...Array(10)].map(_=>Math.ceil(Math.random()*40));
    current = 0;
  }
</script>

<style>
  main {
    font-family: sans-serif;
    text-align: center;
  }
  div {
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: aliceblue;
    border-radius: 50%;
  }

  section {
    display: flex;
    justify-content: center;
    gap: 1rem;
  }

  button{
    padding: 10px 20px;
    border-radius: 10px;
    border: none;
    outline: none;
  }
  button:hover{
    cursor: pointer;
  }
</style>

<main>
	<h1>Selection Sort</h1>
  <section>
    { #each data as item,index }
    <div style="background-color: {sorted || index < current ? 'mediumseagreen' : current===index ? 'orange' : 'dodgerblue'};">{item}</div>
    {/each}
  </section>
    <p>Step: {current} => lowest element found : {lowest}</p>
    <section>
      <button on:click={selectionSort} disabled={sorted}>Run</button>
      <button on:click={reset} disabled={!sorted}>Reset</button>
    </section>
</main>