<script>
	const ask = 'ask.gif';
	const yay = 'yay.gif';
	const sad1 = 'sad1.gif';
	const sad2 = 'sad2.gif';
	const sad3 = 'sad3.gif';
	const sad4 = 'sad4.gif';
	const sad5 = 'sad5.gif';

	const gifs = [sad1, sad2, sad3, sad4, sad5, ask];
	const text = [
		'pleaseee?',
		"don't do this to me :(",
		'wrong button?',
		"you're breaking my heart.",
		'why would you say no???',
		'i thought we had something special!',
		'but what if?',
		"i'm gonna cry...",
		'No'
	];

	let count = 0;
	let yesSize = $state(1.5);
	let noSize = $state(1);
	let resolved = $state(false);
	let bigText = $state('Will you be my Valentine?');

	let currentGifIndex = $state(gifs.length - 1);
	let currentGif = $derived(resolved ? yay : gifs[currentGifIndex]);
	let noTextIndex = $state(text.length - 1);
	let noText = $derived(text[noTextIndex]);

	function yes() {
		resolved = true;
		bigText = 'yayyy!! :3';
	}
	function no() {
		count++;
		yesSize += 0.2;
		noSize *= 0.95;
		if (count < gifs.length - 1) {
			currentGifIndex = count;
		} else {
			let newGifIndex = Math.floor(Math.random() * (gifs.length - 1));
			while (newGifIndex === currentGifIndex) {
				newGifIndex = Math.floor(Math.random() * (gifs.length - 1));
			}
			currentGifIndex = newGifIndex;
		}
		if (count < text.length - 1) {
			noTextIndex = count;
		} else {
			let newNoTextIndex = Math.floor(Math.random() * (text.length - 1));
			while (newNoTextIndex === noTextIndex) {
				newNoTextIndex = Math.floor(Math.random() * (text.length - 1));
			}
			noTextIndex = newNoTextIndex;
		}
	}
</script>

<svelte:head>
	<title>Will You Be My Valentine?</title>
</svelte:head>

<div
	class="flex h-screen flex-col items-center justify-center space-y-8 bg-linear-to-t from-pink-50 to-pink-200 font-sans text-black"
>
	<img class="h-80" src={currentGif} alt="will you be my valentine pleaseeeee?" />
	<h1 class="text-4xl font-bold text-pink-500 italic">{bigText}</h1>
	{#if !resolved}
		<div>
			<button
				class="m-4 inline-block max-h-[50vw] animate-bounce rounded bg-green-500 font-bold text-white hover:bg-green-600"
				style="padding: {24 * yesSize}px; font-size: {24 * yesSize}px;"
				onclick={yes}>Yes!</button
			>
			<button
				class="m-4 rounded bg-red-500 font-bold text-white hover:bg-red-600"
				style="padding: {24 * noSize}px; font-size: {24 * noSize}px;"
				onclick={no}>{noText}</button
			>
		</div>
	{/if}
</div>
