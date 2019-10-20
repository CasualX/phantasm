
<script>
"use strict"

Vue.component('apex-loot', {
	data: function() {
		return {};
	},
	props: {
		state: Object,
		entity: Object,
		local: Object,
	},
	computed: {
		relevant: function() {
			// Only show this loot if it is desired by the local player
			let localPlayer = this.local;
			if (!localPlayer)
				return false;
			if (localPlayer.desired_items[this.entity.custom_script_int] == "1")
				return true;
			let localWeapon = this.state.entity_list.lookup[localPlayer.latest_primary_weapons[0]];
			if (!localWeapon)
				return false;
			if (localWeapon.desired_items[this.entity.custom_script_int] == "1")
				return true;
			return false;
		},
	},
	template: '#apex-loot',
});
</script>

<template id="apex-loot">
	<div class="apex-loot" :style="{ display: relevant ? 'block' : 'none' }"><apex-loot-icon :id="entity.custom_script_int"></apex-loot-icon></div>
</template>

<style>
.apex-loot {
	width: 0px;
	height: 0px;
	overflow: visible;
}
</style>
