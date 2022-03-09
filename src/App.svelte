<script lang="ts">
  let expectancy: number = 80;
  let age: number = 30 * 52;

  const weeks = (year: number, week: number) => {
    return year * 52 + week
  }
</script>

<main>
  <h1>{expectancy}-year life in weeks</h1>
  <svg width="{52*15}" height="{expectancy*15}">
    {#each {length: expectancy} as _, year}
    {#each {length: 52} as _, week}
      <rect x="{week*15}" y="{year*15}" width="10" height="10" stroke="grey" fill={weeks(year, week) < age ? "grey" : "none"} />
    {/each}
    {/each}
  </svg>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
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
