
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
			let primaryWeapon = this.state.entity_list.lookup[localPlayer.primary_weapon];
			if (primaryWeapon && primaryWeapon.desired_items[this.entity.custom_script_int] == "1")
				return true;
			let secondaryWeapon = this.state.entity_list.lookup[localPlayer.secondary_weapon];
			if (secondaryWeapon && secondaryWeapon.desired_items[this.entity.custom_script_int] == "1")
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
