
<script>
"use strict"

Vue.component('mw-player', {
	data: function() {
		return {};
	},
	props: {
		entity: Object,
		cameraEntity: Object,
	},
	methods: {
		selectPlayer: function() {
			this.$emit('select-player', this.entity.index);
		},
	},
	computed: {
		iconStyle: function() {
			let yaw = this.entity.angles[1];
			return {
				'transform': 'rotate(' + (-yaw + 90.0).toString() + 'deg)',
			};
		},
		isLocal: function() {
			return this.cameraEntity == this.entity;
		},
		strokeColor: function() {
			return this.isLocal ? "green" : this.entity.friend ? "blue" : "white";
		},
		X: function() {
			return this.entity.origin[0];
		},
		Y: function() {
			return this.entity.origin[1];
		},
		elevation: function() {
			let cameraEntity = this.cameraEntity;
			if (!cameraEntity) {
				return 0;
			}
			return (this.entity.origin[2] - this.cameraEntity.origin[2]) / 100.0;
		},
	},
	template: '#mw-player',
});
</script>

<template id="mw-player">
	<div class="mw-player">
		<div @click="selectPlayer">
			<svg class="icon" viewBox="-1 -1 2 2" width="20px" height="20px" :style="iconStyle">
				<polygon points="1,0 -0.5,-1 -0.5,-0.5 -1,0 -0.5,0.5 -0.5,1" :stroke="strokeColor" fill="none" stroke-width="0.15" />
			</svg>
			<svg class="elevation" v-if="elevation <= -1.0" style="top: -12px" height="24" viewBox="0 0 24 24" width="24"><path d="M7.41 8.59L12 13.17l4.59-4.58L18 10l-6 6-6-6 1.41-1.41z" fill="red"/></svg>
			<svg class="elevation" v-if="elevation <= -2.5" style="top: -6px" height="24" viewBox="0 0 24 24" width="24"><path d="M7.41 8.59L12 13.17l4.59-4.58L18 10l-6 6-6-6 1.41-1.41z" fill="red"/></svg>
			<svg class="elevation" v-if="elevation >= 1.0" style="top: -12px" height="24" viewBox="0 0 24 24" width="24"><path d="M7.41 15.41L12 10.83l4.59 4.58L18 14l-6-6-6 6 1.41 1.41z" fill="red"/></svg>
			<svg class="elevation" v-if="elevation >= 2.5" style="top: -18px" height="24" viewBox="0 0 24 24" width="24"><path d="M7.41 15.41L12 10.83l4.59 4.58L18 14l-6-6-6 6 1.41 1.41z" fill="red"/></svg>
		</div>
	</div>
</template>

<style>
.mw-player {
	width: 0px;
	height: 0px;
	overflow: visible;
}
.mw-player > div {
	position: relative;
}
.mw-player > div > svg.icon {
	position: absolute;
	transform-origin: center center;
	top: -10px;
	left: -10px;
	z-index: 1;
}
.mw-player > div > svg.elevation {
	position: absolute;
	transform-origin: center center;
	left: 10px;
	z-index: 1;
}
</style>
