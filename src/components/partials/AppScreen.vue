<template>
	<main :class="['app-screen-component']">
		<slot></slot>
	</main>
</template>

<script>
export default {
	name: 'AppScreen',
};
</script>

<style lang="scss">
	.app-screen-component {
		align-items: center;
		display: flex;
		flex-direction: column;
		justify-content: center;
		width: 100%;
		min-height: 100%;

		&:not(.scrollable) {
			height: 100%;
			left: 0;
			overflow: hidden;
			position: fixed;
			top: 0;
			width: 100vw;
		}
	}
</style>
