
<script>
"use strict"

const APEX_RADAR_MATH = {
	'mp_rr_desertlands_64k_x_64k': Object.freeze(new RadarMath(
		[-26123.729, 22965.105, 236, 352],
		[22860.855, -36154.566, 1018, 1297],
		'img/apex/mp_rr_desertlands_64k_x_64k.png', 1350, 1440)),
	'mp_rr_canyonlands_staging': Object.freeze(new RadarMath(
		[-9486.065, 26580.008, 816, 463],
		[28832.563, -27961.234, 2075, 2254],
		'img/apex/mp_rr_canyonlands_staging.jpg', 2483, 2483)),
	'mp_rr_canyonlands_mu1_night': Object.freeze(new RadarMath(
		[-9486.065, 26580.008, 816, 463],
		[28832.563, -27961.234, 2075, 2254],
		'img/apex/mp_rr_canyonlands_staging.jpg', 2483, 2483)),
};

Vue.component('apex-radar', {
	data: function() {
		return {};
	},
	props: {
		state: Object,
		camera: CameraStore,
	},
	computed: {
		radarMath: function() {
			if (this.state == null) {
				return null;
			}
			return APEX_RADAR_MATH[this.state.client_state.level_name];
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
			let fraction = Math.max(Math.min((this.state.globals.curtime - world.death_field_time_start) / (world.death_field_time_end - world.death_field_time_start), 1.0), 0.0);
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
				let player_resources = this.entities[this.state.entity_list.player_resources];
				if (player_resources) {
					let index = player_resources.names.indexOf(this.camera.follow);
					player = this.entities[index];
				}
			}
			// Fall back to the local player if no follow name is specified.
			if (player == null) {
				player = this.entities[this.state.globals.local_entity];
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
			<apex-loot v-for="entity in lootEntities" :key="entity.entity_ptr" :state="state" :entity="entity" :local="cameraPlayer" :camera="camera" :style="{ transform: entityTranslate(entity.origin) }"></apex-loot>
			<apex-player v-for="entity in playerEntities" :key="entity.entity_ptr" :state="state" :entity="entity" :local="cameraPlayer" :camera="camera" :style="{ transform: entityTranslate(entity.origin) }"></apex-player>
		</div>
		<p class="text-stroke--outline">{{ state.client_state.level_name }}</p>
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
