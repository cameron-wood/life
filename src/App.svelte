<script lang="ts">
  const now = new Date();
  const today = new Date(now.getUTCFullYear(), now.getUTCMonth(), now.getUTCDate());

  let expectancy: number = 80;
  let dob: string = new Date().toISOString().split("T")[0];

  let diffTime: number;
  let diffWeeks: number;
  $: diffTime = today.valueOf() - new Date(dob).valueOf();
  $: diffWeeks = diffTime / (1000 * 60 * 60 * 24 * 7);

  const fill = (year: number, week: number, ageWeeks: number): string => {
    const weekNumber = year * 52 + week;

    if (weekNumber < Math.floor(ageWeeks)) {
      return "grey";
    } else if (weekNumber < Math.ceil(ageWeeks)) {
      return "lightgray";
    } else {
      return "none";
    }
  }
</script>

<main>
  <label for="dob">Date of Birth</label>
  <input type="date" id="dob" bind:value={dob}>
  <h1>{expectancy}-year life in weeks</h1>
  <svg width="{52*15}" height="{expectancy*15}">
    {#each {length: expectancy} as _, year}
    {#each {length: 52} as _, week}
      <!-- <circle cx="{week*15+5}" cy="{year*15+5}" r="5" stroke="darkgrey" fill={fill(year, week, diffWeeks)}/> -->
      <rect x="{week*15}" y="{year*15}" width="10" height="10" stroke="darkgrey" fill={fill(year, week, diffWeeks)}/>
    {/each}
    {/each}
  </svg>
  <footer>
    <p>Inspired by Tim Urban's <a href="https://waitbutwhy.com/2014/05/life-weeks.html" target="_blank">Your Life in Weeks - Wait But Why</a></p>
  </footer>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 800px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
