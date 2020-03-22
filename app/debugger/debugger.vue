
<script>
"use strict"

Vue.component('app-debugger', {
	data() {
		return {
			component: 'debug-state',
			panel: null,
		};
	},
	props: {
		socket: WebSocketStore,
	},
	methods: {
		togglePause() {
			this.socket.paused = !this.socket.paused;
		},
		click(panel) {
			if (panel) {
				this.component = 'debug-xss';
				this.panel = panel;
			}
			else {
				this.component = 'debug-state';
				this.panel = null;
			}
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
			<button @click="click(null)">State</button>
			<template v-for="panel in Object.keys(socket.debugText)">
				<button @click="click(panel)">{{ panel }}</button>
			</template>
		</form>
		<debug-state v-if="component == 'debug-state'" :state="socket.state"></debug-state>
		<debug-xss v-if="component == 'debug-xss'" :html="socket.debugText[panel]"></debug-xss>
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
