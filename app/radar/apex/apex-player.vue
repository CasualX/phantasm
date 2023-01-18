
<script>
"use strict"

Vue.component('apex-player', {
	data: function() {
		return {};
	},
	props: {
		state: Object,
		entity: Object,
		local: Object,
		camera: CameraStore,
	},
	computed: {
		playerName: function() {
			return this.state.name_list[(this.entity.index - 1) * 2] || "";
		},
		followMe: function() {
			return this.entity == this.local;
		},
		color: function() {
			if (this.followMe) {
				return 'white';
			}
			let rgb = this.entity.team_color;
			return `rgb(${rgb[0]}, ${rgb[1]}, ${rgb[2]})`;
		},
		armorText: function() {
			// return "" + this.entity.armor_type;
			return this.entity.armor_type > 0 ? "" + this.entity.armor_type : null;
		},
		iconStyle: function() {
			let yaw = this.state.client.local_entity == this.entity.index ? -this.entity.camera_angles[1] : -this.entity.angles[1];
			return {
				'transform': 'rotate(' + yaw + 'deg)',
				'stroke-width': this.followMe ? '0.1' : '0.05',
			};
		},
		playerStyle: function() {
			return {
				'display': this.entity.life_state == 0 ? 'block' : 'none',
				'opacity': this.entity.bleedout_state == 0 ? '1.0' : '0.4',
				'transform': this.followMe ? 'scale(1.1)' : 'scale(1.0)',
			};
		},
	},
	template: '#apex-player',
});
</script>

<template id="apex-player">
	<div class="apex-player">
		<div :style="playerStyle">
			<svg viewBox="-1 -1 2 2" width="20px" height="20px" :style="iconStyle">
				<polygon points="1,0 -1,-0.75 -0.25,0 -1,0.75" stroke="black" :fill="color" />
			</svg>
			<span class="armor text-stroke--outline">{{ armorText }}</span>
			<span v-if="camera.showNames" class="name text-stroke--outline">{{ playerName }}</span>
		</div>
	</div>
</template>

<style>
.apex-player {
	width: 0px;
	height: 0px;
	overflow: visible;
}
.apex-player > div {
	position: relative;
}
.apex-player > div > svg {
	position: absolute;
	transform-origin: center center;
	top: -10px;
	left: -10px;
	z-index: 1;
}
.apex-player > div > span.name {
	position: absolute;
	top: 10px;
	left: -20px;
	z-index: -1;

	color: white;
	font-size: 0.8rem;
	white-space: nowrap;
}
.apex-player > div > span.armor {
	position: absolute;
	top: -5px;
	left: -2px;
	z-index: 2;

	color: white;
	font-size: 8px;
	white-space: nowrap;
}
</style>
