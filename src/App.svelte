<script>
  import logo from './assets/svelte.png'
  import Routine from './lib/Routine.svelte'
	import { invoke } from "@tauri-apps/api/tauri"

	import ChromaPicker from 'svelte-chroma-picker'
import { xlink_attr } from 'svelte/internal'

	let color = '#fff'
  let darkbg = []

	
	let rgb;
  let gradient = [];
  let orig_gradient  = [];

	const handleColorUpdate = ev => {
		rgb = ev.detail.rgb;
		invoke("generate_gradient", rgb).then(([grad,orig_grad]) => {
			gradient = grad;
      orig_gradient = orig_grad;
      console.log(gradient);
		});
	};

  function get_dark() {
    console.log("huh1");
    invoke("send_dark").then((dark) =>{
      console.log(dark)
      darkbg = dark
    });
  }


</script>

<main>
  <button style="background:rgb({darkbg[0]}, {darkbg[1]}, {darkbg[2]})" on:click="{get_dark}"> lmao </button>
	<ChromaPicker bind:color on:update="{handleColorUpdate}"/>
  <div class="holder">
    <div class="left">
    {#each gradient as color}

      <div style="background:rgb({color[0]}, {color[1]}, {color[2]})">
        {color[0]}, {color[1]}, {color[2]}
      </div>
    {/each}
    </div>

    <div class="right">
      {#each orig_gradient as color}
  
        <div style="background:rgb({color[0]}, {color[1]}, {color[2]})">
          {color[0]}, {color[1]}, {color[2]}
        </div>
      {/each}
    </div>
    <div>
    </div>
  </div>
  <Routine />
</main>

<style>
  .holder{
    display:flex;

  }

  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }
</style>
