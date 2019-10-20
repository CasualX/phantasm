
<script>
"use strict"

Vue.component('debug-xss', {
	data: function() {
		return {};
	},
	props: {
		html: String,
	},
	template: '#debug-xss',
});
</script>

<template id="debug-xss">
	<div class="debug-xss" v-html="html"></div>
</template>

<style>
.debug-xss {
	margin: 1rem;
}
</style>
