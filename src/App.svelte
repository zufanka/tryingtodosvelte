<script>
	
	import { LayerCake, Html } from 'layercake';

	import BubbleChart from './BubbleChart.svelte';

  	import data from './data.js';

	import Scrolly from "./Scrolly.svelte";

    
	let value;
	

	const idKey = 'country';
	const valueKey = 'expenses'; 

	/* convert all the values into a number */
	data.forEach(d => {
		d["expenses"] = +d["expenses"];
		/* console.log(d[valueKey], +d[valueKey])*/
	});

	data.forEach(d => {
		d["approved"] = +d["approved"];
		/* console.log(d[valueKey], +d[valueKey])*/
	});
	

</script>

<section>
	<div class="section-container">
		<div class="sticky">
			<LayerCake
			padding={{ top: 0, bottom: 20, left: 30 }}
			data={data}
			>
			<Html>
				<BubbleChart
				idKey={idKey}
				valueKey={valueKey}
				fill='#ff00cc'
				stroke='#9f0080'
				textColor='#61004e'
				textStroke='#ffdbf8'
				textStrokeWidth={1}
				step={value}
				/>
			</Html>
			</LayerCake>
		</div>
		<div class="steps-container">
			<Scrolly bind:value>
				{#each [1,2,3] as text, i}
					<div class="step" class:active={value === i}>
						<div class="step-content">
							<p>Step {text}</p>
						</div>
					</div>
				{/each}

			</Scrolly>
		</div>	
		
	</div>
</section>




<style>
	:global(body) {
		overflow-x: hidden;
	}
	
	.hero {
		height: 60vh;
		display: flex;
		place-items: center;
		flex-direction: column;
		justify-content: center;
		text-align: center;
	}
	
	.hero h2 {
		margin-top: 0;
		font-weight: 200;
	}
	
  .spacer {
    height: 40vh;
  }

  .sticky {
    position: sticky;
    top: 5%;
	flex: 1 1 100%;
	height: 90vh;
  }

  .section-container {
    margin-top: 1em;
    text-align: center;
    transition: background 100ms;
    display: flex;
	flex-wrap: wrap;
  }

  .step {
    height: 80vh;
    display: flex;
    place-items: center;
    justify-content: center;
  }

  .step-content {
    font-size: 1rem;
    background: whitesmoke;
    color: #ccc;
    border-radius: 5px;
    padding: .5rem 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    transition: background 500ms ease;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, .2);
    text-align: left;
		width: 75%;
		margin: auto;
		max-width: 500px;
  }

	.step.active .step-content {
		background: white;
		color: black;
	}
	

  .steps-container {
    flex: 1 1 100%;
    z-index: 10;
  }
	
/* Comment out the following line to always make it 'text-on-top' */
  @media screen and (max-width: 768px) {
    .section-container {
      flex-direction: column-reverse;
    }
    .sticky {
      width: 95%;
			margin: auto;
    }
  }
</style>