<script>
	import Stuff from '../lib/stuff.svelte';
	export const prerender = true;
</script>

<div class="container">
	<h1>Dune re-read progress indicator</h1>
	<p>
		Not sure what this is? Join the Dune discord. <a href="https://discord.gg/dune" target="_blank">
			https://discord.gg/dune
		</a>
	</p>
	<p>Either way, the chapters must flow.</p>

	<hr />

	<div>
		<!-- <p><strong>Book One</strong></p>
		<p>week 1: Chapter 1-7 "A beginning..."</p>
		<p>week 2: Chapter 8-15 "Yueh! Yueh! Yueh!"</p>
		<p>week 3: Chapter 16-22 "Greatness is a transitory experience"</p>
		<p><strong>Book Two: Muad'Dib</strong></p>
		<p>week 4: Chapter 23-30 "When my father, the Padishah Emperor..."</p>
		<p>week 5: Chapter 31-37 "Prophecy and prescience"</p>
		<p><strong>Book Three: The Prophet</strong></p>
		<p>week 6: Chapter 38-43 "No woman, no man, no child..."</p>
		<p>week 7: Chapter 44-48 "How often it is"</p> -->
		<p><strong>-July 9 -</strong> Week 0; Find a copy of Dune Messiah</p>
		<p>
			<strong>-July 16 -</strong> Week 1; Read Prologue + Ch. 1-5 "such a rich store of myths..."
		</p>
		<p>
			<strong>-July 23-</strong> Week 2; Discuss Week 1 reading, Read Ch. 6-12 "Once more the drama begins"
		</p>
		<p>
			<strong>-July 30 -</strong> Week 3; Discuss Week 2 reading, Read Ch. 13-19 "I've had a bellyful
			of the god and priest business!"
		</p>
		<p>
			<strong>-August 6 -</strong> Week 4; Discuss Week 3 reading, Read Ch. 20-24 + Epilogue "Tibana
			was an apologist for Socratic Christianity..."
		</p>
		<p><strong>-August 13 -</strong> Discuss Week 4's reading</p>
	</div>

	<hr />

	<Stuff />
</div>

<style>
	.container {
		width: 90%;
		max-width: 800px;
		margin: 90px auto;
	}
	hr {
		margin: 40px 0;
	}
</style>
