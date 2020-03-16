
<script>
"use strict"

Vue.component('app-radar', {
	data: function() {
		return {
			camera: new CameraStore(),
		};
	},
	props: {
		socket: Object,
	},
	computed: {
		component: function() {
			switch (this.socket.game) {
				case 'apex':
					return 'apex-radar';
				case 'mw':
					return 'mw-radar';
				default:
					return null;
			}
		},
	},
	methods: {
		fullscreen: function(e) {
			this.$refs.radar.requestFullscreen();
		},
	},
	template: '#app-radar',
});
</script>

<template id="app-radar">
	<div class="app-radar">
		<form @submit.prevent="" class="user-select--none">
			<h3>Settings</h3>
			<label>Zoom:<input type="range" v-model="camera.zoom" min="0.5" max="3.0" step="any"></label>
			<label>Follow:<input type="text" v-model="camera.follow"></label>
			<label><input type="checkbox" v-model="camera.showNames" />Show player names</label>
			<label><button @click="fullscreen">Fullscreen</button></label>
		</form>
		<section ref="radar">
			<component v-if="component" :is="component" :state="socket.state" :camera="camera"></component>
			<div v-else>
				<template v-if="socket.game">
					<p>Now playing {{ socket.game }}.</p>
					<p>This game is not yet supported.</p>
				</template>
				<p v-else>Waiting for host to start playing...</p>
			</div>
		</section>
	</div>
</template>

<style>
.app-radar {
	display: grid;
	grid-template: auto / 14rem auto;
}
.app-radar > section {
	background-color: white;
	overflow: hidden;
}
.app-radar > form {
	display: flex;
	flex-direction: column;
	padding: 1rem;
}
.app-radar > form > label {
	margin-top: 0.5rem;
}
</style>
