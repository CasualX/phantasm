
<script>
"use strict"

Vue.component('mw-player', {
	data: function() {
		return {};
	},
	props: {
		state: Object,
		entity: Object,
	},
	computed: {
		iconStyle: function() {
			let yaw = this.entity.angles[1];
			return {
				'transform': 'rotate(' + (-yaw + 90.0).toString() + 'deg)',
			};
		},
		isLocal: function() {
			return this.state.entities.local_index == this.entity.index;
		},
		strokeColor: function() {
			if (this.isLocal) {
				return "green";
			}
			else {
				return "white";
			}
		},
		fillColor: function() {
			if (this.isLocal) {
				return "rgb(50,50,50)";
			}
			else {
				return "black";
			}
		},
		X: function() {
			return this.entity.origin[0];
		},
		Y: function() {
			return this.entity.origin[1];
		},
	},
	template: '#mw-player',
});
</script>

<template id="mw-player">
	<div class="mw-player">
		<div>
			<svg viewBox="-1 -1 2 2" width="20px" height="20px" :style="iconStyle">
				<polygon points="1,0 -0.5,-1 -0.5,-0.5 -1,0 -0.5,0.5 -0.5,1" :stroke="strokeColor" :fill="fillColor" stroke-width="0.15" />
			</svg>
			<!-- <p style="color: white;">{{ X }}</p> -->
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
.mw-player > div > svg {
	position: absolute;
	transform-origin: center center;
	top: -10px;
	left: -10px;
	z-index: 1;
}
</style>
