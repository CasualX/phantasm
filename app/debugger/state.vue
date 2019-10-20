
<script>
"use strict"

Vue.component('debug-state', {
	data: function() {
		return {
			choice: {},
		};
	},
	props: {
		state: Object,
	},
	computed: {
		groups: function() {
			let groups = [];
			if (this.state != null) {
				const stringify = (name, object) => {
					// Classify the keys of the object
					let valueKeys = [];
					let objectKeys = [];
					for (let [key, value] of Object.entries(object)) {
						if (value instanceof Array) {
							if (value.length > 0) {
								if (typeof value[0] == "object") {
									objectKeys.push(key);
								}
								else {
									valueKeys.push(key);
								}
							}
							else {
								valueKeys.push(key);
							}
						}
						else if (value instanceof Object) {
							objectKeys.push(key);
						}
						else {
							valueKeys.push(key);
						}
					}
					if (valueKeys.length > 0) {
						let keyWidth = Math.max.apply(null, valueKeys.map(key => key.length)) + 2;
						let text = valueKeys.map(key => (key + ": ").padEnd(keyWidth) + object[key]).join("\n");
						groups.push({
							name: name,
							text: text,
						});
					}
					for (let key of objectKeys) {
						let childName = name == "Root" ? key : name + "." + key;
						if (object[key] instanceof Array) {
							let index = this.choice[childName];
							groups.push({
								name: childName,
								index: index,
							});
							let child = object[key][index];
							if (child != null) {
								stringify(childName + "[" + index + "]", child);
							}
						}
						else if (object[key] instanceof Object) {
							stringify(childName, object[key]);
						}
					}
				}
				stringify("Root", this.state);
			}
			return groups;
		},
	},
	methods: {
		setChoice: function(key, value) {
			Vue.set(this.choice, key, value);
		},
	},
	template: '#debug-state',
});
</script>

<template id="debug-state">
	<div class="debug-state">
		<template v-for="group in groups">
			<h3>{{ group.name }}</h3>
			<pre v-if="'text' in group">{{ group.text }}</pre>
			<label><input v-if="'index' in group" type="text" @input="setChoice(group.name, $event.target.value)" ></label>
		</template>
	</div>
</template>

<style>
.debug-state {
	margin: 1rem;
}
.debug-state > pre {
	white-space: pre-wrap;
	word-break: break-all;
}
</style>
