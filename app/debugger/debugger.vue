
<script>
"use strict"

Vue.component('app-debugger', {
	data: function() {
		return {
			component: 'debug-state',
		};
	},
	props: {
		socket: WebSocketStore,
	},
	methods: {
		togglePause: function() {
			this.socket.paused = !this.socket.paused;
		},
	},
	template: '#app-debugger',
});
</script>

<template id="app-debugger">
	<div class="app-debugger">
		<form @submit.prevent="">
			<button v-if="socket.paused" @click="togglePause">Unpause</button>
			<button v-if="!socket.paused" @click="togglePause">Pause</button>
			<button @click="component = 'debug-state'">State</button>
			<button @click="component = 'debug-xss'">XSS</button>
		</form>
		<debug-state v-if="component == 'debug-state'" :state="socket.state"></debug-state>
		<debug-xss v-if="component == 'debug-xss'" :html="socket.debugText"></debug-xss>
	</div>
</template>

<style>
.app-debugger {
	display: grid;
	grid-template: auto / 14rem auto;
}
.app-debugger > form {
	display: flex;
	flex-direction: column;
	margin: 1rem;
}
</style>
