<script>
	import book from '../book.json';

	const weeks = [
		range(1, 7),
		range(8, 15),
		range(16, 22),
		range(23, 30),
		range(31, 37),
		range(38, 43),
		range(44, 48)
	];

	const startDate = '14 may 2023 00:00';
	const now = new Date();

	const weeksWithInfo = weeks.map((week, i) => {
		let d = new Date(startDate);
		d.setDate(d.getDate() + 7 * i);
		const weekAfter = new Date(d.getTime());
		weekAfter.setDate(weekAfter.getDate() + 7);

		// (10-5)/(15-5)
		const progressInWeekBase = (now.getTime() - d.getTime()) / (weekAfter.getTime() - d.getTime());

		const progressInWeek = Math.max(0, Math.min(1, progressInWeekBase));

		return {
			weekNo: i + 1,
			startDate: d,
			chapters: week.map((chNo, i2) => {
				const percentageInWeek = (1 / week.length) * i2;
				return {
					chNo,
					percentageInWeek,
					progressInWeek,
					weekNo: i + 1
				};
			}),
			progressInWeek
		};
	});

	const allChapters = weeksWithInfo.flatMap((w) => w.chapters);
	allChapters.map((ch, i) => {
		// References babyy!
		let value = ch.progressInWeek;
		let chapterStart = ch.percentageInWeek;
		let chapterEnd = allChapters[i + 1]?.percentageInWeek || 1;

		// I can't do math
		let percentageUntilNext = (value - chapterStart) / (chapterEnd - chapterStart);

		ch.percentageUntilNext = Math.min(1, Math.max(0, percentageUntilNext));

		ch.hasRead = ch.percentageUntilNext > 0;
	});

	function range(a, b) {
		return Array(b - a + 1)
			.fill(0)
			.map((_, i) => i + a);
	}
</script>

{#each weeksWithInfo as week}
	<div class="week">
		<h2>Week {week.weekNo}</h2>
		{#each week.chapters as { chNo, hasRead, percentageUntilNext }}
			{@const chapter = book.find((t) => t.ch === chNo)}
			<div class="chapter">
				<div class="left">
					<div class="ball" has-read={hasRead} />
					<div class="line" style={`--height: ${percentageUntilNext * 100}%`} />
				</div>
				<div>
					<p>Chapter {chNo}</p>
					<p class="quote">
						{@html chapter.quote
							.split('\n')
							.map((t) => (t.startsWith('-') ? `<strong>${t}</strong>` : t))
							.join('\n')}
					</p>
				</div>
			</div>
		{/each}
	</div>
{/each}

<style>
	.chapter {
		display: grid;
		grid-template-columns: 16px 1fr;
		grid-gap: 20px;
		margin: 30px 0;
		--gray: #bcbcbc;
		--green: rgb(54, 137, 54);
	}

	.ball {
		width: 100%;
		aspect-ratio: 1/1;
		background: var(--gray);
		border-radius: 50%;
		position: relative;
		z-index: 10;
	}
	.ball[has-read='true'] {
		background: var(--green);
	}

	.line {
		width: 2px;
		margin-top: -8px;
		height: calc(100% + 8px + 20px);
		margin-left: calc(16px / 2 - 2px / 2);
		z-index: -1;
		background: linear-gradient(to bottom, var(--green) var(--height), var(--gray) var(--height));
	}

	.week .chapter:last-child .line {
		border-radius: 10px;
		height: 50%;
	}

	.chapter div p:first-child {
		margin-top: 0;
	}
	.chapter div p:last-child {
		margin-bottom: 0;
	}

	.quote {
		white-space: pre-wrap;
	}

	@media (prefers-color-scheme: dark) {
		.chapter {
			--gray: #474747;
		}
	}
</style>
