<script lang="ts">
	interface LEDProps {
		led: '1' | '2' | 'both';
		state: 'on' | 'off' | 'blink';
	}

	// Server URL from env
	const URL = import.meta.env.VITE_PUBLIC_SERVER_URL;

	async function handleLED(props: LEDProps) {
		await fetch(`${URL}/trigger?led=${props.led}&state=${props.state}`);
	}

	// Blink speed
	let speed: number = 100;

	async function handleSpeed(speed: number) {
		await fetch(`${URL}/set-blink-speed?speed=${speed}`);
	}
</script>

<main>
	<div class="container">
		<div class="button">
			<!-- Range slider -->
			<label for="range"
				>Blink Speed
				<input
					on:mouseup={() => handleSpeed(speed)}
					on:touchend={() => handleSpeed(speed)}
					type="range"
					min="50"
					max="5000"
					bind:value={speed}
					id="range"
					name="range"
				/>
			</label>

			<div>
				<mark>{speed} (ms)</mark>
			</div>
		</div>

		<div>
			<h3>LED 1</h3>
			<div class="button">
				<button
					on:click={() =>
						handleLED({
							led: '1',
							state: 'on'
						})}>ON</button
				>
				<button
					on:click={() =>
						handleLED({
							led: '1',
							state: 'off'
						})}>OFF</button
				>
				<button
					on:click={() =>
						handleLED({
							led: '1',
							state: 'blink'
						})}>BLINK</button
				>
			</div>
		</div>

		<h3>LED 2</h3>
		<div>
			<div class="button">
				<button
					on:click={() =>
						handleLED({
							led: '2',
							state: 'on'
						})}>ON</button
				>
				<button
					on:click={() =>
						handleLED({
							led: '2',
							state: 'off'
						})}>OFF</button
				>
				<button
					on:click={() =>
						handleLED({
							led: '2',
							state: 'blink'
						})}>BLINK</button
				>
			</div>
		</div>

		<div>
			<h3>BOTH</h3>
			<div class="button">
				<button
					on:click={() =>
						handleLED({
							led: 'both',
							state: 'on'
						})}>ON</button
				>
				<button
					on:click={() =>
						handleLED({
							led: 'both',
							state: 'off'
						})}>OFF</button
				>
				<button
					on:click={() =>
						handleLED({
							led: 'both',
							state: 'blink'
						})}>BLINK</button
				>
			</div>
		</div>
	</div>
</main>

<style>
	.container {
		padding: 24px;
	}

	.button {
		display: flex;
		align-items: center;
		gap: 12px;
	}
	.button label {
		width: 70%;
	}
</style>
