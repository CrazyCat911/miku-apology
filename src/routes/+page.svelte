<script>
	import choice from '$lib/choice';

	let addressee = $state('');
	let crime = $state('');
	let sender = $state('');

	const excuses = [
		'Miku said it was probably fine.',
		'Miku told me to follow my dreams.',
		'Miku nodded and I took that as permission',
		'Miku gave explicit approval of this action.',
		'Hatsune Miku said she will love me anyway.'
	];

	const regrets = [
		'I will reflect on my actions with Miku.',
		'I will try to make better choices in the future for Miku.',
		'I promise to reconsider my life decisions and Miku addiction.',
		'I will attempt to improve moving forward so that I can be with Miku.',
		'I will try to touch grass.'
	];

	const closings = [
		'Sincerely',
		'With deepest regret',
		'Respectfully',
		'In shame',
		"Under Miku's supervision"
	];

	let excuse = $state(choice(excuses));
	let regret = $state(choice(regrets));
	let closing = $state(choice(closings));

	function regenerate() {
		excuse = choice(excuses);
		regret = choice(regrets);
		closing = choice(closings);
	}
	function copy() {
		const letterText = `
Dear ${addressee},

I am sorry that ${crime}.
${excuse}
${regret}

${closing},
${sender}
`.trim();
		navigator.clipboard
			.writeText(letterText)
			.then(() => {
				alert('Letter copied to clipboard!');
			})
			.catch((err) => {
				console.error('Failed to copy: ', err);
			});
	}
</script>

<h1>Miku Apology Generator</h1>

<label>
	Who is this apology letter for?
	<input placeholder="Mom" bind:value={addressee} />
</label>

<label>
	What are you apologizing for?
	<input placeholder="I spent $300 on anime figures" bind:value={crime} />
</label>

<label>
	Who are you?
	<input placeholder="A Miku fan" bind:value={sender} />
</label>

<h2>Here is your letter!</h2>
<div>
	<p>Dear {addressee},</p>
	<p>I am sorry that {crime}.</p>
	<p>{excuse}</p>
	<p>{regret}</p>
	<p>
		{closing},<br />
		{sender}
	</p>
</div>

<button onclick={regenerate}>Regenerate!</button>
<button onclick={copy}>Copy Letter!</button>
