
<script>
"use strict"

const APEX_ITEMS = Object.freeze({
	GOLD_KRABER: 1,
	GOLD_MASTIFF: 2,
	LSTAR: 3,
	HAVOC: 4,
	GOLD_HAVOC: 5,
	DEVOTION: 6,
	TRIPLE_TAKE: 7,
	GOLD_TRIPLE_TAKE: 8,
	FLATLINE: 9,
	GOLD_FLATLINE: 10,
	HEMLOCK: 11,
	G7_SCOUT: 12,
	GOLD_G7_SCOUT: 13,
	ALTERNATOR: 14,
	GOLD_ALTERNATOR: 15,
	R99: 16,
	PROWLER: 17,
	GOLD_PROWLER: 18,
	LONGBOW: 19,
	GOLD_LONGBOW: 20,
	CHARGE_RIFLE: 21,
	GOLD_CHARGE_RIFLE: 22,
	SPITFIRE: 23,
	R301: 24,
	EVA8_AUTO: 26,
	GOLD_EVA8_AUTO: 27,
	PEACEKEEPER: 28,
	GOLD_PEACEKEEPER: 29,
	MOZAMBIQUE: 30,
	GOLD_MOZAMBIQUE: 31,
	WINGMAN: 32,
	GOLD_WINGMAN: 33,
	P2020: 34,
	GOLD_P2020: 35,
	RE45: 36,
	GOLD_RE45: 37,

	LIGHT_ROUNDS: 40,
	ENERGY_AMMO: 41,
	SHOTGUN_SHELLS: 42,
	HEAVY_ROUNDS: 43,
	SNIPER_AMMO: 44,

	ULTIMATE_ACCELERANT: 45,
	PHOENIX_KIT: 46,
	MED_KIT: 47,
	SYRINGE: 48,
	SHIELD_BATTERY: 49,
	SHIELD_CELL: 50,

	HELMET_LV1: 51,
	HELMET_LV2: 52,
	HELMET_LV3: 53,
	HELMET_LV4: 54,
	BODY_ARMOR_LV1: 55,
	BODY_ARMOR_LV2: 56,
	BODY_ARMOR_LV3: 57,
	BODY_ARMOR_LV4: 58,
	EVO_ARMOR_LV1: 59,
	EVO_ARMOR_LV2: 60,
	EVO_ARMOR_LV3: 61,
	EVO_ARMOR_LV4: 62,
	KNOCKDOWN_SHIELD_LV1: 63,
	KNOCKDOWN_SHIELD_LV2: 64,
	KNOCKDOWN_SHIELD_LV3: 65,
	KNOCKDOWN_SHIELD_LV4: 66,
	BACKPACK_LV1: 67,
	BACKPACK_LV2: 68,
	BACKPACK_LV3: 69,
	BACKPACK_LV4: 70,

	THERMITE_GRENADE: 71,
	FRAG_GRENADE: 72,
	ARC_STAR: 73,

	HCOG_CLASSIC: 74,
	HCOG_BRUISER: 75,
	HOLO: 76,
	VARIABLE_HOLO: 77,
	DIGITAL_THREAT: 78,
	HCOG_RANGER: 79,
	VARIABLE_AOG: 80,
	SNIPER: 81,
	VARIABLE_SNIPER: 82,
	DIGITAL_SNIPER_THREAT: 83,

	BARREL_STABILIZER_LV1: 84,
	BARREL_STABILIZER_LV2: 85,
	BARREL_STABILIZER_LV3: 86,
	BARREL_STABILIZER_LV4: 87,
	LIGHT_MAGAZINE_LV1: 88,
	LIGHT_MAGAZINE_LV2: 89,
	LIGHT_MAGAZINE_LV3: 90,
	HEAVY_MAGAZINE_LV1: 91,
	HEAVY_MAGAZINE_LV2: 92,
	HEAVY_MAGAZINE_LV3: 93,
	SNIPER_MAGAZINE_LV1: 94,
	SNIPER_MAGAZINE_LV2: 95,
	SNIPER_MAGAZINE_LV3: 96,
	SHOTGUN_BOLT_LV1: 97,
	SHOTGUN_BOLT_LV2: 98,
	SHOTGUN_BOLT_LV3: 99,
	STANDARD_STOCK_LV1: 100,
	STANDARD_STOCK_LV2: 101,
	STANDARD_STOCK_LV3: 102,
	SNIPER_STOCK_LV1: 103,
	SNIPER_STOCK_LV2: 104,
	SNIPER_STOCK_LV3: 105,

	SELECTFIRE_RECEIVER: 106,
	PRECISION_CHOKE: 107,
	HAMMERPOINT_ROUNDS: 108,
	ANVIL_RECEIVER: 109,
	DOUBLE_TAP_TRIGGER: 110,
	VAULT_KEY: 111,
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
				case APEX_ITEMS.SHOTGUN_BOLT_LV1:
				case APEX_ITEMS.STANDARD_STOCK_LV1:
				case APEX_ITEMS.SNIPER_STOCK_LV1:
					return 'common';
				case APEX_ITEMS.BARREL_STABILIZER_LV2:
				case APEX_ITEMS.LIGHT_MAGAZINE_LV2:
				case APEX_ITEMS.HEAVY_MAGAZINE_LV2:
				case APEX_ITEMS.SNIPER_MAGAZINE_LV2:
				case APEX_ITEMS.SHOTGUN_BOLT_LV2:
				case APEX_ITEMS.STANDARD_STOCK_LV2:
				case APEX_ITEMS.SNIPER_STOCK_LV2:
					return 'rare';
				case APEX_ITEMS.BARREL_STABILIZER_LV3:
				case APEX_ITEMS.LIGHT_MAGAZINE_LV3:
				case APEX_ITEMS.HEAVY_MAGAZINE_LV3:
				case APEX_ITEMS.SNIPER_MAGAZINE_LV3:
				case APEX_ITEMS.SHOTGUN_BOLT_LV3:
				case APEX_ITEMS.STANDARD_STOCK_LV3:
				case APEX_ITEMS.SNIPER_STOCK_LV3:
					return 'epic';
				case APEX_ITEMS.BARREL_STABILIZER_LV4:
					return 'legendary'

				case APEX_ITEMS.SELECTFIRE_RECEIVER:
					return 'epic';
				case APEX_ITEMS.PRECISION_CHOKE:
					return 'epic';
				case APEX_ITEMS.HAMMERPOINT_ROUNDS:
					return 'epic';
				case APEX_ITEMS.ANVIL_RECEIVER:
					return 'legendary'
				case APEX_ITEMS.DOUBLE_TAP_TRIGGER:
					return 'epic';
				case APEX_ITEMS.VAULT_KEY:
					return 'special';

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
				case APEX_ITEMS.HEAVY_MAGAZINE_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Extended_Heavy_Mag.svg?version=638867e063a508db86a48a03142e20dd';
				case APEX_ITEMS.HEAVY_MAGAZINE_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Extended_Heavy_Mag.svg?version=638867e063a508db86a48a03142e20dd';
				case APEX_ITEMS.HEAVY_MAGAZINE_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Extended_Heavy_Mag.svg?version=638867e063a508db86a48a03142e20dd';
				case APEX_ITEMS.SNIPER_MAGAZINE_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=e8f41174d8b4dcd715818c516262b6fa';
				case APEX_ITEMS.SNIPER_MAGAZINE_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=e8f41174d8b4dcd715818c516262b6fa';
				case APEX_ITEMS.SNIPER_MAGAZINE_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/2/21/Extended_Energy_Mag.svg?version=e8f41174d8b4dcd715818c516262b6fa';
				case APEX_ITEMS.SHOTGUN_BOLT_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/ba/Shotgun_Bolt.svg?version=2dc6778ff0833154873ecf16ba3cac8c';
				case APEX_ITEMS.SHOTGUN_BOLT_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/ba/Shotgun_Bolt.svg?version=2dc6778ff0833154873ecf16ba3cac8c';
				case APEX_ITEMS.SHOTGUN_BOLT_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/ba/Shotgun_Bolt.svg?version=2dc6778ff0833154873ecf16ba3cac8c';
				case APEX_ITEMS.STANDARD_STOCK_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/c2/Standard_Stock.svg?version=959ea0351bf14ee9e0e864e839fa42f7';
				case APEX_ITEMS.STANDARD_STOCK_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/c2/Standard_Stock.svg?version=959ea0351bf14ee9e0e864e839fa42f7';
				case APEX_ITEMS.STANDARD_STOCK_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/c/c2/Standard_Stock.svg?version=959ea0351bf14ee9e0e864e839fa42f7';
				case APEX_ITEMS.SNIPER_STOCK_LV1: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/0/09/Sniper_Stock.svg?version=7a70f08f7f3e6b97d58306430d0f1263';
				case APEX_ITEMS.SNIPER_STOCK_LV2: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/0/09/Sniper_Stock.svg?version=7a70f08f7f3e6b97d58306430d0f1263';
				case APEX_ITEMS.SNIPER_STOCK_LV3: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/0/09/Sniper_Stock.svg?version=7a70f08f7f3e6b97d58306430d0f1263';

				case APEX_ITEMS.SELECTFIRE_RECEIVER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/7/72/Selectfire_Receiver.svg?version=155f8c34324f67df4fb32c7fedafdccc';
				case APEX_ITEMS.PRECISION_CHOKE: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/b/b4/Precision_Choke.svg?version=c9c72c08b6ebd9335bbaa75d02b93ddb';
				case APEX_ITEMS.HAMMERPOINT_ROUNDS: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/d/d4/Hammerpoint_Rounds.svg?version=2a64cdceffe6c28787f6f50929d9d350';
				case APEX_ITEMS.ANVIL_RECEIVER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/5/5d/Anvil_Receiver.svg?version=9a8f4067114a3a50a1beb9b6ad493722';
				case APEX_ITEMS.DOUBLE_TAP_TRIGGER: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/9/9b/Double_Tap_Trigger.svg?version=351da015b0d06624c9b3ae5e2d790727';
				case APEX_ITEMS.VAULT_KEY: return 'https://gamepedia.cursecdn.com/apexlegends_gamepedia_en/5/59/Vault_Key.svg?version=de07ef3a8227114372dc80fe4ac36c6d';

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
