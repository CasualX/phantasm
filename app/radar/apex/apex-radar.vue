
<script>
"use strict"

const APEX_RADAR_MATH = {
	'mp_rr_desertlands_64k_x_64k': Object.freeze(new RadarMath(
		[-26123.729, 22965.105, 236, 352],
		[22860.855, -36154.566, 1018, 1297],
		'img/apex/mp_rr_desertlands_64k_x_64k.png', 1350, 1440)),
	'mp_rr_desertlands_64k_x_64k_tt': Object.freeze(new RadarMath(
		[-26123.729, 22965.105, 236, 352],
		[22860.855, -36154.566, 1018, 1297],
		'img/apex/mp_rr_desertlands_64k_x_64k.png', 1350, 1440)),
	'mp_rr_desertlands_mu1': Object.freeze(new RadarMath(
		[-26123.729, 22965.105, 236, 352],
		[22860.855, -36154.566, 1018, 1297],
		'img/apex/mp_rr_desertlands_64k_x_64k.png', 1350, 1440)),
	'mp_rr_desertlands_mu2': Object.freeze(new RadarMath(
		[-26123.729, 22965.105, 433, 502],
		[22860.855, -36154.566, 1539, 1844],
		'img/apex/mp_rr_desertlands_mu2.webp', 2048, 2048)),
	'mp_rr_desertlands_mu3': Object.freeze(new RadarMath(
		[-26123.729, 22965.105, 433, 502],
		[22860.855, -36154.566, 1539, 1844],
		'img/apex/mp_rr_desertlands_mu3.webp', 2048, 2048)),
	'mp_rr_canyonlands_staging': Object.freeze(new RadarMath(
		[-9486.065, 26580.008, 816, 463],
		[28832.563, -27961.234, 2075, 2254],
		'img/apex/mp_rr_canyonlands_staging.jpg', 2483, 2483)),
		'mp_rr_canyonlands_mu1_night': Object.freeze(new RadarMath(
		[-9486.065, 26580.008, 816, 463],
		[28832.563, -27961.234, 2075, 2254],
	'img/apex/mp_rr_canyonlands_staging.jpg', 2483, 2483)),
		'mp_rr_canyonlands_mu1': Object.freeze(new RadarMath(
		[-9486.065, 26580.008, 816, 463],
		[28832.563, -27961.234, 2075, 2254],
		'img/apex/mp_rr_canyonlands_staging.jpg', 2483, 2483)),
	'mp_rr_canyonlands_64k_x_64k': Object.freeze(new RadarMath(
		[-9486.065, 26580.008, 816, 463],
		[28832.563, -27961.234, 2075, 2254],
		'img/apex/mp_rr_canyonlands_staging.jpg', 2483, 2483)),
	'mp_rr_canyonlands_mu2': Object.freeze(new RadarMath(
		[-9486.065, 26580.008, 816, 463],
		[28832.563, -27961.234, 2075, 2254],
		'img/apex/mp_rr_canyonlands_staging.jpg', 2483, 2483)),
	'mp_rr_canyonlands_hu': Object.freeze(new RadarMath(
		[-9486.065, 26580.008, 816, 463],
		[28832.563, -27961.234, 2075, 2254],
		'img/apex/mp_rr_canyonlands_staging.jpg', 2483, 2483)),
	'mp_rr_canyonlands_mu3': Object.freeze(new RadarMath(
		[-27502.287, 24504.262, 246, 487],
		[25764.455, -24487.516, 1583, 1707],
		'img/apex/mp_rr_canyonlands_mu3.webp', 2048, 2008)),
	'mp_rr_olympus': Object.freeze(new RadarMath(
		[-20723.979, 33996.98, 711, 319],
		[25053.246, -22165.426, 1751, 1595],
		'img/apex/mp_rr_olympus.webp', 2048, 2048)),
	'mp_rr_olympus_mu2': Object.freeze(new RadarMath(
		[-20723.979, 33996.98, 711 * 2.078125, 319 * 2.078125],
		[25053.246, -22165.426, 1751 * 2.078125, 1595 * 2.078125],
		'img/apex/mp_rr_olympus_mu2.png', 4256, 4256)),
	'mp_rr_tropic_island_mu1': Object.freeze(new RadarMath(
		[44519.77, 27817.998, 941, 239],
		[-37277.574, -22472.045, 134, 741],
		'img/apex/ApexLegendsStormPoint_inside_1.webp', 1014, 1007)),
	'mp_rr_divided_moon': Object.freeze(new RadarMath(
		[28228.582, 31701.05, 1757, 283],
		[-29679.441, -25812.479, 367, 1662],
		'img/apex/Broken_Moon.webp', 2048, 2048)),
};

Vue.component('apex-radar', {
	data: function() {
		return {};
	},
	props: {
		state: Object,
		other: Object,
		camera: CameraStore,
		apexrings: Array,
	},
	computed: {
		radarMath: function() {
			if (this.state == null) {
				return null;
			}
			return APEX_RADAR_MATH[this.state.client.level_name];
		},
		entities: function() {
			if (this.state == null) {
				return [];
			}
			return this.state.entity_list.lookup;
		},
		worldEntity: function() {
			return this.entities[0];
		},
		worldStyle: function() {
			let world = this.worldEntity;
			if (!world || !world.death_field_is_active || world.death_field_time_start == world.death_field_time_end) {
				return {
					display: 'none',
				};
			}
			let fraction = Math.max(Math.min((this.state.client.curtime - world.death_field_time_start) / (world.death_field_time_end - world.death_field_time_start), 1.0), 0.0);
			let radius = world.death_field_radius_start + fraction * (world.death_field_radius_end - world.death_field_radius_start);
			let [x, y, r] = this.radarMath.circleToPixel(world.death_field_origin, radius);
			let zoom = this.camera.zoom;
			return {
				overflow: 'visible',
				left: (x - r) * zoom + 'px',
				top: (y - r) * zoom + 'px',
				width: r * 2 * zoom + 'px',
				height: r * 2 * zoom + 'px',
			};
		},
		lootEntities: function() {
			if (this.state == null) {
				return [];
			}
			return this.state.entity_list.entities.filter(value => value.class_name == 'PropSurvival');
		},
		playerEntities: function() {
			if (this.state == null) {
				return [];
			}
			return this.state.entity_list.entities.filter(value => value.class_name == 'Player');
		},
		cameraPlayer: function() {
			if (this.state == null) {
				return null;
			}
			let player = null;
			// Try to find the player to follow by their name.
			if (this.camera.follow) {
				let index = this.state.name_list.indexOf(this.camera.follow);
				if (index >= 0) {
					player = this.entities[index / 2 + 1];
				}
			}
			// Fall back to the local player if no follow name is specified.
			if (player == null) {
				player = this.entities[this.state.client.local_entity];
			}
			// If the playing being followed is dead, follow whomever they are spectating.
			if (player && player.life_state != 0 && player.observer_target > 0) {
				player = this.entities[player.observer_target];
			}
			return player;
		},
		cameraTranslate: function() {
			let player = this.cameraPlayer;
			if (!player || !this.$refs.canvas) {
				return 'translate(0,0)';
			}
			let [px, py] = this.radarMath.toPixel(player.origin);
			let zoom = this.camera.zoom;
			let bounds = this.$refs.canvas.getBoundingClientRect();
			let tx = -px * zoom + bounds.width / 2;
			let ty = -py * zoom + bounds.height / 2;
			return 'translate(' + tx + 'px,' + ty + 'px)';
		},
		cameraScale: function() {
			return 'scale(' + this.camera.zoom + ')';
		},
	},
	methods: {
		entityTranslate: function(origin) {
			let [px, py] = this.radarMath.toPixel(origin);
			let zoom = this.camera.zoom;
			return 'translate(' + px * zoom + 'px,' + py * zoom + 'px)';
		},
		ringStyle: function(ring) {
			let [x, y, r] = this.radarMath.circleToPixel(ring.origin, ring.radius);
			let zoom = this.camera.zoom;
			return {
				overflow: 'visible',
				left: (x - r) * zoom + 'px',
				top: (y - r) * zoom + 'px',
				width: r * 2 * zoom + 'px',
				height: r * 2 * zoom + 'px',
			};
		},
	},
	template: '#apex-radar',
});
</script>

<template id="apex-radar">
	<div class="apex-radar user-select--none" ref="canvas">
		<div v-if="radarMath" class="apex-radar__canvas" :style="{ transform: cameraTranslate }">
			<img :src="radarMath.url" :style="{ transform: `scale(${camera.zoom})` }">
			<svg viewBox="-1 -1 2 2" :style="worldStyle">
				<circle cx="0" cy="0" r="1" stroke="red" fill="none" vector-effect="non-scaling-stroke" stroke-width="2" />
			</svg>
			<svg v-for="ring in apexrings" :key="ring.radius" :style="ringStyle(ring)">
				<circle cx="0" cy="0" r="1" stroke="green" fill="none" vector-effect="non-scaling-stroke" stroke-width="2"/>
			</svg>
			<!-- <apex-loot v-for="entity in lootEntities" :key="entity.entity_ptr" :state="state" :entity="entity" :local="cameraPlayer" :camera="camera" :style="{ transform: entityTranslate(entity.origin) }"></apex-loot> -->
			<apex-player v-for="entity in playerEntities" :key="entity.entity_ptr" :state="state" :entity="entity" :local="cameraPlayer" :camera="camera" :style="{ transform: entityTranslate(entity.origin) }"></apex-player>
		</div>
		<p class="text-stroke--outline">{{ state.client.level_name }}</p>
	</div>
</template>

<style>
.apex-radar {
	width: 100%;
	height: 100%;
	background-color: #2c3238;
	position: relative;
}
.apex-radar__canvas {
	position: relative;
}
.apex-radar__canvas > img {
	transform-origin: top left;
}
.apex-radar__canvas > * {
	position: absolute;
	left: 0;
	top: 0;
}
.apex-radar > p {
	position: absolute;
	right: 0;
	bottom: 0;
	color: white;
	margin: 0.5rem;
}
</style>
