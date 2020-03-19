
<script>
"use strict"

Vue.component('mw-radar', {
	data: function() {
		return {
			cameraIndex: null,
		};
	},
	props: {
		state: Object,
		camera: CameraStore,
	},
	computed: {
		entities: function() {
			if (this.state == null) {
				return [];
			}
			return this.state.entities_data.list;
		},
		playerEntities: function() {
			return this.entities.filter(entity => entity.valid && entity.type == 1);
		},
		cameraEntity: function() {
			if (this.state == null) {
				return null;
			}
			let index = this.cameraIndex == null ? this.state.entities_data.local_index : this.cameraIndex;
			let entity = this.entities[index];
			if (this.state.entities_data.local_index == entity.index) {
				entity.origin = this.state.cg.origin;
			}
			return entity;
		},
	},
	methods: {
		entityTranslate: function(origin) {
			let cameraEntity = this.cameraEntity;
			let local = cameraEntity ? cameraEntity.origin : this.state.cg.origin;
			let zoom = 0.05 / this.camera.zoom;
			let x = origin[1] - local[1];
			let y = origin[0] - local[0];

			let canvas = document.getElementById('mw-canvas-ref');
			//let bounds = this.$refs.canvas.getBoundingClientRect();
			if (!canvas) {
				return 'translate(0,0)';
			}
			let bounds = canvas.getBoundingClientRect();
			let tx = x * zoom + bounds.width / 2;
			let ty = y * zoom + bounds.height / 2;
			return 'translate(' + tx + 'px,' + ty + 'px)';
		},
		selectPlayer: function(playerIndex) {
			this.cameraIndex = this.cameraIndex === playerIndex ? null : playerIndex;
		},
	},
	template: '#mw-radar',
});
</script>

<template id="mw-radar">
	<div class="mw-radar user-select--none" ref="canvas" id="mw-canvas-ref">
		<div class="mw-radar__canvas">
			<mw-player v-for="entity in playerEntities" :key="entity.index" :entity="entity" :camera-entity="cameraEntity" @select-player="selectPlayer($event)" :style="{ transform: entityTranslate(entity.origin) }" ></mw-player>
		</div>
	</div>
</template>

<style>
.mw-radar {
	width: 100%;
	height: 100%;
	position: relative;
	background-color: black;
}
.mw-radar__canvas {
	position: relative;
	background-color: black;
}
.mw-radar__canvas > * {
	position: absolute;
	left: 0;
	top: 0;
}
</style>
