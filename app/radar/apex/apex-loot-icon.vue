
<script>
"use strict"

const APEX_ITEMS = Object.freeze({
	LIGHT_ROUNDS: 121,
	ENERGY_AMMO: 122,
	SHOTGUN_SHELLS: 123,
	HEAVY_ROUNDS: 124,
	SNIPER_AMMO: 125,

	ULTIMATE_ACCELERANT: 162,
	PHOENIX_KIT: 163,
	MED_KIT: 164,
	SYRINGE: 165,
	SHIELD_BATTERY: 166,
	SHIELD_CELL: 167,

	HELMET_LV1: 168,
	HELMET_LV2: 169,
	HELMET_LV3: 170,
	HELMET_LV4: 171,
	BODY_ARMOR_LV1: 172,
	BODY_ARMOR_LV2: 173,
	BODY_ARMOR_LV3: 174,
	BODY_ARMOR_LV4: 175,
	EVO_ARMOR_LV0: 176,
	EVO_ARMOR_LV1: 177,
	EVO_ARMOR_LV2: 178,
	EVO_ARMOR_LV3: 179,
	EVO_ARMOR_LV4: 180,
	KNOCKDOWN_SHIELD_LV1: 182,
	KNOCKDOWN_SHIELD_LV2: 183,
	KNOCKDOWN_SHIELD_LV3: 184,
	KNOCKDOWN_SHIELD_LV4: 185,
	BACKPACK_LV1: 186,
	BACKPACK_LV2: 187,
	BACKPACK_LV3: 188,
	BACKPACK_LV4: 189,

	THERMITE_GRENADE: 190,
	FRAG_GRENADE: 191,
	ARC_STAR: 192,

	HCOG_CLASSIC: 193,
	HCOG_BRUISER: 194,
	HOLO: 195,
	VARIABLE_HOLO: 196,
	DIGITAL_THREAT: 197,
	HCOG_RANGER: 198,
	VARIABLE_AOG: 199,
	SNIPER: 200,
	VARIABLE_SNIPER: 201,
	DIGITAL_SNIPER_THREAT: 202,

	BARREL_STABILIZER_LV1: 203,
	BARREL_STABILIZER_LV2: 204,
	BARREL_STABILIZER_LV3: 205,
	BARREL_STABILIZER_LV4: 206,
	LIGHT_MAGAZINE_LV1: 207,
	LIGHT_MAGAZINE_LV2: 208,
	LIGHT_MAGAZINE_LV3: 209,
	LIGHT_MAGAZINE_LV4: 210,
	HEAVY_MAGAZINE_LV1: 211,
	HEAVY_MAGAZINE_LV2: 212,
	HEAVY_MAGAZINE_LV3: 213,
	HEAVY_MAGAZINE_LV4: 214,
	ENERGY_MAGAZINE_LV1: 215,
	ENERGY_MAGAZINE_LV2: 216,
	ENERGY_MAGAZINE_LV3: 217,
	ENERGY_MAGAZINE_LV4: 218,
	SNIPER_MAGAZINE_LV1: 219,
	SNIPER_MAGAZINE_LV2: 220,
	SNIPER_MAGAZINE_LV3: 221,
	SNIPER_MAGAZINE_LV4: 222,
	SHOTGUN_BOLT_LV1: 223,
	SHOTGUN_BOLT_LV2: 224,
	SHOTGUN_BOLT_LV3: 225,
	STANDARD_STOCK_LV1: 226,
	STANDARD_STOCK_LV2: 227,
	STANDARD_STOCK_LV3: 228,
	SNIPER_STOCK_LV1: 229,
	SNIPER_STOCK_LV2: 230,
	SNIPER_STOCK_LV3: 231,

	TURBOCHARGER: 232,
	SKULLPIERCER_RIFLING: 233,
	HAMMERPOINT_ROUNDS: 234,
});
const APEX_ITEMS_LOOKUP = (function() {
	let lookup = [];
	for (let [key, value] of Object.entries(APEX_ITEMS)) {
		lookup[value] = key;
	}
	return Object.freeze(lookup);
})();

Vue.component('apex-loot-icon', {
	data: function() {
		return {
			items: APEX_ITEMS,
			lookup: APEX_ITEMS_LOOKUP,
		};
	},
	props: {
		id: Number,
	},
	computed: {
		color: function() {
			switch (this.id) {
				case APEX_ITEMS.HELMET_LV1:
				case APEX_ITEMS.BODY_ARMOR_LV1:
				case APEX_ITEMS.EVO_ARMOR_LV1:
				case APEX_ITEMS.KNOCKDOWN_SHIELD_LV1:
				case APEX_ITEMS.BACKPACK_LV1:
					return 'common';
				case APEX_ITEMS.HELMET_LV2:
				case APEX_ITEMS.BODY_ARMOR_LV2:
				case APEX_ITEMS.EVO_ARMOR_LV2:
				case APEX_ITEMS.KNOCKDOWN_SHIELD_LV2:
				case APEX_ITEMS.BACKPACK_LV2:
					return 'rare';
				case APEX_ITEMS.HELMET_LV3:
				case APEX_ITEMS.BODY_ARMOR_LV3:
				case APEX_ITEMS.EVO_ARMOR_LV3:
				case APEX_ITEMS.KNOCKDOWN_SHIELD_LV3:
				case APEX_ITEMS.BACKPACK_LV3:
					return 'epic';
				case APEX_ITEMS.HELMET_LV4:
				case APEX_ITEMS.BODY_ARMOR_LV4:
				case APEX_ITEMS.EVO_ARMOR_LV4:
				case APEX_ITEMS.KNOCKDOWN_SHIELD_LV4:
				case APEX_ITEMS.BACKPACK_LV4:
					return 'legendary';

				case APEX_ITEMS.HCOG_CLASSIC:
				case APEX_ITEMS.HOLO:
					return 'common';
				case APEX_ITEMS.HCOG_BRUISER:
				case APEX_ITEMS.VARIABLE_HOLO:
				case APEX_ITEMS.SNIPER:
					return 'rare';
				case APEX_ITEMS.HCOG_RANGER:
				case APEX_ITEMS.VARIABLE_AOG:
				case APEX_ITEMS.VARIABLE_SNIPER:
					return 'epic';
				case APEX_ITEMS.DIGITAL_THREAT:
				case APEX_ITEMS.DIGITAL_SNIPER_THREAT:
					return 'legendary';

				case APEX_ITEMS.BARREL_STABILIZER_LV1:
				case APEX_ITEMS.LIGHT_MAGAZINE_LV1:
				case APEX_ITEMS.HEAVY_MAGAZINE_LV1:
				case APEX_ITEMS.SNIPER_MAGAZINE_LV1:
				case APEX_ITEMS.ENERGY_MAGAZINE_LV1:
				case APEX_ITEMS.SHOTGUN_BOLT_LV1:
				case APEX_ITEMS.STANDARD_STOCK_LV1:
				case APEX_ITEMS.SNIPER_STOCK_LV1:
					return 'common';
				case APEX_ITEMS.BARREL_STABILIZER_LV2:
				case APEX_ITEMS.LIGHT_MAGAZINE_LV2:
				case APEX_ITEMS.HEAVY_MAGAZINE_LV2:
				case APEX_ITEMS.SNIPER_MAGAZINE_LV2:
				case APEX_ITEMS.ENERGY_MAGAZINE_LV2:
				case APEX_ITEMS.SHOTGUN_BOLT_LV2:
				case APEX_ITEMS.STANDARD_STOCK_LV2:
				case APEX_ITEMS.SNIPER_STOCK_LV2:
					return 'rare';
				case APEX_ITEMS.BARREL_STABILIZER_LV3:
				case APEX_ITEMS.LIGHT_MAGAZINE_LV3:
				case APEX_ITEMS.HEAVY_MAGAZINE_LV3:
				case APEX_ITEMS.SNIPER_MAGAZINE_LV3:
				case APEX_ITEMS.ENERGY_MAGAZINE_LV3:
				case APEX_ITEMS.SHOTGUN_BOLT_LV3:
				case APEX_ITEMS.STANDARD_STOCK_LV3:
				case APEX_ITEMS.SNIPER_STOCK_LV3:
					return 'epic';
				case APEX_ITEMS.BARREL_STABILIZER_LV4:
				case APEX_ITEMS.LIGHT_MAGAZINE_LV4:
				case APEX_ITEMS.HEAVY_MAGAZINE_LV4:
				case APEX_ITEMS.SNIPER_MAGAZINE_LV4:
				case APEX_ITEMS.ENERGY_MAGAZINE_LV4:
					return 'legendary'

				case APEX_ITEMS.HAMMERPOINT_ROUNDS:
					return 'epic';
				case APEX_ITEMS.SKULLPIERCER_RIFLING:
					return 'legendary'

				default:
					return null;
			}
		},
		imgClass: function() {
			let classes = [];
			if (this.color) {
				classes.push(this.color);
			}
			return classes;
		},
		url: function() {
			// https://apexlegends.gamepedia.com/Category:Icons
			switch (this.id) {
				case APEX_ITEMS.ENERGY_AMMO: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/2d/Energy_Ammo.svg?version=390e43edd3090b2028a803464d9b0adb';
				case APEX_ITEMS.LIGHT_ROUNDS: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/a/a5/Light_Rounds.svg?version=fc9faab38694bc023271ff726a274324';
				case APEX_ITEMS.SHOTGUN_SHELLS: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/4/42/Shotgun_Shells.svg?version=241ad6a7fc4f53cfd0e5d99a4931f0b1';
				case APEX_ITEMS.HEAVY_ROUNDS: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/5/55/Heavy_Rounds.svg?version=33c68df7515676ea25e49ac581943c23';
				case APEX_ITEMS.SNIPER_AMMO: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/5/55/Heavy_Rounds.svg?version=33c68df7515676ea25e49ac581943c23';

				case APEX_ITEMS.ULTIMATE_ACCELERANT: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/e/e5/Ultimate_Accelerant.svg?version=7b8cb618912fab8c213106cf1c5f4b6e';
				case APEX_ITEMS.PHOENIX_KIT: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/7/7b/Phoenix_Kit.svg?version=89a9a183a0db308beb13ab438ca62e1d';
				case APEX_ITEMS.MED_KIT: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/d/d3/Medkit.svg?version=21cb266bacb1458169c3f0f65e023256';
				case APEX_ITEMS.SYRINGE: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/7/75/Syringe.svg?version=81b223aafdd8cc7226f48b4bcbb3c186';
				case APEX_ITEMS.SHIELD_BATTERY: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/d/de/Shield_Battery.svg?version=b305b2ef32f04524d313c3490ff0e07e';
				case APEX_ITEMS.SHIELD_CELL: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/4/4a/Shield_Cell.svg?version=b31c210d33027e2ad11b32959c6b62b8';

				case APEX_ITEMS.HELMET_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/e/e8/Helmet.svg?version=bda6c6aa84dda6fc6bdf60f3a832496e';
				case APEX_ITEMS.HELMET_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/e/e8/Helmet.svg?version=bda6c6aa84dda6fc6bdf60f3a832496e';
				case APEX_ITEMS.HELMET_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/e/e8/Helmet.svg?version=bda6c6aa84dda6fc6bdf60f3a832496e';
				case APEX_ITEMS.HELMET_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/e/e8/Helmet.svg?version=bda6c6aa84dda6fc6bdf60f3a832496e';
				case APEX_ITEMS.BODY_ARMOR_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/cc/Body_Shield.svg?version=a6d68fb3e0d64d4b5adad9ed6341fcb9';
				case APEX_ITEMS.BODY_ARMOR_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/cc/Body_Shield.svg?version=a6d68fb3e0d64d4b5adad9ed6341fcb9';
				case APEX_ITEMS.BODY_ARMOR_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/cc/Body_Shield.svg?version=a6d68fb3e0d64d4b5adad9ed6341fcb9';
				case APEX_ITEMS.BODY_ARMOR_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/cc/Body_Shield.svg?version=a6d68fb3e0d64d4b5adad9ed6341fcb9';
				case APEX_ITEMS.EVO_ARMOR_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/cc/Body_Shield.svg?version=a6d68fb3e0d64d4b5adad9ed6341fcb9';
				case APEX_ITEMS.EVO_ARMOR_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/cc/Body_Shield.svg?version=a6d68fb3e0d64d4b5adad9ed6341fcb9';
				case APEX_ITEMS.EVO_ARMOR_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/cc/Body_Shield.svg?version=a6d68fb3e0d64d4b5adad9ed6341fcb9';
				case APEX_ITEMS.EVO_ARMOR_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/cc/Body_Shield.svg?version=a6d68fb3e0d64d4b5adad9ed6341fcb9';
				case APEX_ITEMS.KNOCKDOWN_SHIELD_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/3/34/Knockdown_Shield.svg?version=ad80680b065e870c67ba38e5945c702c';
				case APEX_ITEMS.KNOCKDOWN_SHIELD_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/3/34/Knockdown_Shield.svg?version=ad80680b065e870c67ba38e5945c702c';
				case APEX_ITEMS.KNOCKDOWN_SHIELD_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/3/34/Knockdown_Shield.svg?version=ad80680b065e870c67ba38e5945c702c';
				case APEX_ITEMS.KNOCKDOWN_SHIELD_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/3/34/Knockdown_Shield.svg?version=ad80680b065e870c67ba38e5945c702c';
				case APEX_ITEMS.BACKPACK_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/26/Backpack_lvl1.svg?version=bd7234e811250e3c5d7956da2a18389f';
				case APEX_ITEMS.BACKPACK_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/bc/Backpack_lvl2.svg?version=b3810f10abf47b3b7c59a37ce36c7227';
				case APEX_ITEMS.BACKPACK_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/8/8f/Backpack_lvl3.svg?version=22ef37fd8cbefae2bfc905a66dc53d86';
				case APEX_ITEMS.BACKPACK_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/8/8f/Backpack_lvl3.svg?version=22ef37fd8cbefae2bfc905a66dc53d86';

				case APEX_ITEMS.THERMITE_GRENADE: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/a/ae/Thermite_Grenade.svg?version=6d23ae5a4341afe09968b416e750c4bf';
				case APEX_ITEMS.FRAG_GRENADE: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/c6/Frag_Grenade.svg?version=93e085163284cf7956f3d52eeb7e2845';
				case APEX_ITEMS.ARC_STAR: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/d/d8/Arc_Star.svg?version=f057e28435c241c969ae20d7096d49b7';

				case APEX_ITEMS.HCOG_CLASSIC: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9a/1x_HCOG_Classic.svg?version=ab723c377f5f8ec8c203e4e468ef7985';
				case APEX_ITEMS.HCOG_BRUISER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/f/f3/2x_HCOG_Bruiser.svg?version=3da2fe94523d3e13fc12dacf94c6081f';
				case APEX_ITEMS.HOLO: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/e/e5/1x_Holo.svg?version=b88b85591a40e88917de3516a1615f33';
				case APEX_ITEMS.VARIABLE_HOLO: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/5/5b/1x-2x_Variable_Holo.svg?version=3cb35921da152948d03b9cd9f325fd68';
				case APEX_ITEMS.DIGITAL_THREAT: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/4/42/1x_Digital_Threat.svg?version=245bb7091b71cf956a4f5f7d00c41d6d';
				case APEX_ITEMS.HCOG_RANGER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/8/8a/3x_HCOG_Ranger.svg?version=384801b2a532db136ade975b519c9510';
				case APEX_ITEMS.VARIABLE_AOG: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/2f/2x-4x_Variable_AOG.svg?version=588eef11d4b1843d4e26e3a52d4ce898';
				case APEX_ITEMS.SNIPER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/3/3f/6x_Sniper.svg?version=4b0ec37d31300a6dbf269bfc26980c15';
				case APEX_ITEMS.VARIABLE_SNIPER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/d/dc/4x-8x_Variable_Sniper.svg?version=6ef2ffd4185a2b77a0b24d0071c00d03';
				case APEX_ITEMS.DIGITAL_SNIPER_THREAT: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/f/f8/4x-10x_Digital_Sniper_Threat.svg?version=f1bcd0a4467dbd519a8657fc52d930e4';

				case APEX_ITEMS.BARREL_STABILIZER_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/99/Barrel_Stabilizer.svg?version=db6460847e7fac0208aeb2d64e2bcc56';
				case APEX_ITEMS.BARREL_STABILIZER_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/99/Barrel_Stabilizer.svg?version=db6460847e7fac0208aeb2d64e2bcc56';
				case APEX_ITEMS.BARREL_STABILIZER_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/99/Barrel_Stabilizer.svg?version=db6460847e7fac0208aeb2d64e2bcc56';
				case APEX_ITEMS.BARREL_STABILIZER_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/ba/Barrel_Stabilizer_lvl4.svg?version=44d8ed563da9501b50cf721bddb9b59f';
				case APEX_ITEMS.LIGHT_MAGAZINE_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/8/85/Extended_Light_Mag.svg?version=5ecf3b445f2a6e456488ead829c52825';
				case APEX_ITEMS.LIGHT_MAGAZINE_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/8/85/Extended_Light_Mag.svg?version=5ecf3b445f2a6e456488ead829c52825';
				case APEX_ITEMS.LIGHT_MAGAZINE_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/8/85/Extended_Light_Mag.svg?version=5ecf3b445f2a6e456488ead829c52825';
				case APEX_ITEMS.LIGHT_MAGAZINE_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/8/85/Extended_Light_Mag.svg?version=5ecf3b445f2a6e456488ead829c52825';
				case APEX_ITEMS.HEAVY_MAGAZINE_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Extended_Heavy_Mag.svg?version=638867e063a508db86a48a03142e20dd';
				case APEX_ITEMS.HEAVY_MAGAZINE_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Extended_Heavy_Mag.svg?version=638867e063a508db86a48a03142e20dd';
				case APEX_ITEMS.HEAVY_MAGAZINE_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Extended_Heavy_Mag.svg?version=638867e063a508db86a48a03142e20dd';
				case APEX_ITEMS.HEAVY_MAGAZINE_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Extended_Heavy_Mag.svg?version=638867e063a508db86a48a03142e20dd';
				case APEX_ITEMS.ENERGY_MAGAZINE_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=2b31a07cffcf4a6b277923af7e6bfe8b';
				case APEX_ITEMS.ENERGY_MAGAZINE_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=2b31a07cffcf4a6b277923af7e6bfe8b';
				case APEX_ITEMS.ENERGY_MAGAZINE_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=2b31a07cffcf4a6b277923af7e6bfe8b';
				case APEX_ITEMS.ENERGY_MAGAZINE_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=2b31a07cffcf4a6b277923af7e6bfe8b';
				case APEX_ITEMS.SNIPER_MAGAZINE_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=e8f41174d8b4dcd715818c516262b6fa';
				case APEX_ITEMS.SNIPER_MAGAZINE_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=e8f41174d8b4dcd715818c516262b6fa';
				case APEX_ITEMS.SNIPER_MAGAZINE_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=e8f41174d8b4dcd715818c516262b6fa';
				case APEX_ITEMS.SNIPER_MAGAZINE_LV4: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=e8f41174d8b4dcd715818c516262b6fa';
				case APEX_ITEMS.SHOTGUN_BOLT_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/ba/Shotgun_Bolt.svg?version=2dc6778ff0833154873ecf16ba3cac8c';
				case APEX_ITEMS.SHOTGUN_BOLT_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/ba/Shotgun_Bolt.svg?version=2dc6778ff0833154873ecf16ba3cac8c';
				case APEX_ITEMS.SHOTGUN_BOLT_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/ba/Shotgun_Bolt.svg?version=2dc6778ff0833154873ecf16ba3cac8c';
				case APEX_ITEMS.STANDARD_STOCK_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/c2/Standard_Stock.svg?version=959ea0351bf14ee9e0e864e839fa42f7';
				case APEX_ITEMS.STANDARD_STOCK_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/c2/Standard_Stock.svg?version=959ea0351bf14ee9e0e864e839fa42f7';
				case APEX_ITEMS.STANDARD_STOCK_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/c2/Standard_Stock.svg?version=959ea0351bf14ee9e0e864e839fa42f7';
				case APEX_ITEMS.SNIPER_STOCK_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/0/09/Sniper_Stock.svg?version=7a70f08f7f3e6b97d58306430d0f1263';
				case APEX_ITEMS.SNIPER_STOCK_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/0/09/Sniper_Stock.svg?version=7a70f08f7f3e6b97d58306430d0f1263';
				case APEX_ITEMS.SNIPER_STOCK_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/0/09/Sniper_Stock.svg?version=7a70f08f7f3e6b97d58306430d0f1263';

				// case APEX_ITEMS.SELECTFIRE_RECEIVER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/7/72/Selectfire_Receiver.svg?version=155f8c34324f67df4fb32c7fedafdccc';
				// case APEX_ITEMS.PRECISION_CHOKE: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/b4/Precision_Choke.svg?version=c9c72c08b6ebd9335bbaa75d02b93ddb';
				// case APEX_ITEMS.HAMMERPOINT_ROUNDS: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/d/d4/Hammerpoint_Rounds.svg?version=2a64cdceffe6c28787f6f50929d9d350';
				// case APEX_ITEMS.SKULLPIERCER_RIFLING: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/ce/Skullpiercer_Rifling.svg?version=3c45ac7e2dee0f4f9e5bbb18ff5ef96d';
				// case APEX_ITEMS.DOUBLE_TAP_TRIGGER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Double_Tap_Trigger.svg?version=351da015b0d06624c9b3ae5e2d790727';
				// case APEX_ITEMS.VAULT_KEY: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/5/59/Vault_Key.svg?version=de07ef3a8227114372dc80fe4ac36c6d';

				default: return null;
			}
		},
	},
	template: '#apex-loot-icon',
});
</script>

<template id="apex-loot-icon">
	<div class="apex-loot-icon"><img v-if="url" :class="imgClass" :src="url"></div>
</template>

<style>
.apex-loot-icon {
	position: relative;
	width: 0px;
	height: 0px;
	overflow: visible;
}
.apex-loot-icon > img {
	position: absolute;
	/* width: 16px; */
	height: 16px;
	left: -8px;
	top: -8px;
}
.apex-loot-icon > img.common {
	filter: grayscale(100%) brightness(150%) drop-shadow(0 0 1px white);
}
.apex-loot-icon > img.rare {
	filter: grayscale(100%) brightness(150%) sepia(100%) hue-rotate(-180deg) saturate(1000%) drop-shadow(0 0 1px white);
}
.apex-loot-icon > img.epic {
	filter: grayscale(100%) brightness(150%) sepia(100%) hue-rotate(-100deg) saturate(1000%) drop-shadow(0 0 1px white);
}
.apex-loot-icon > img.legendary {
	filter: grayscale(100%) brightness(150%) sepia(100%) hue-rotate(5deg) saturate(1000%) drop-shadow(0 0 1px white);
}
.apex-loot-icon > img.special {
	filter: grayscale(100%) brightness(150%) sepia(100%) hue-rotate(-50deg) saturate(1000%) drop-shadow(0 0 1px white);
}
</style>
