<template>
	<div id="app">
		<div>
			<IsInputNumber
				mode="plus-minus"
				:max="2"
				:min="1"
				:disabled="false"
				:value.sync="value"
				@change="onChange"
			/>
		</div>
	</div>
</template>

<script>
import IsInputNumber from './components/IsInputNumber.vue';

export default {
	name: 'App',
	components: {
		IsInputNumber,
	},
	data() {
		return {
			value: 0,
		}
	},
	methods: {
		onChange(value) {
			this.value = value;
		},
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
