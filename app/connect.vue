
<script>
"use strict"

Vue.component('app-connect', {
	data: function() {
		return {};
	},
	props: {
		socket: Object,
	},
	computed: {
		connecting: function() {
			return this.socket.socket != null;
		},
		shareURL: function() {
			let share = window.location.href.split("#")[0] +
				"#address=" + encodeURIComponent(this.socket.address) +
				"&username=" + encodeURIComponent(this.socket.username) +
				"&secret=" + encodeURIComponent(this.socket.secret);
			return share;
		},
	},
	methods: {
		submit: function(e) {
			if (this.connecting) {
				this.socket.disconnect();
			}
			else {
				this.socket.connect();
			}
		},
	},
	mounted: function() {
		let args = argv();
		if ('address' in args) {
			this.socket.address = args.address;
		}
		if ('username' in args) {
			this.socket.username = args.username;
		}
		if ('secret' in args) {
			this.socket.secret = args.secret;
		}
	},
	template: '#app-connect',
});
</script>

<template id="app-connect">
	<div class="app-connect">
		<p>Please start by connecting to a host.</p>
		<form @submit.prevent="submit">
			<label>Address:</label>
			<input type="text" v-model="socket.address" :readonly="connecting" :disabled="connecting">
			<span class="error">{{ socket.error }}</span>
			<label>Username:</label>
			<input type="text" v-model="socket.username" :readonly="connecting" :disabled="connecting">
			<label>Secret:</label>
			<input type="password" v-model="socket.secret" :readonly="connecting" :disabled="connecting">
			<label>Share:</label>
			<input type="text" :value="shareURL" readonly="readonly">
			<label></label>
			<input v-if="!connecting" type="submit" value="Connect">
			<input v-if="connecting" type="submit" value="Disconnect">
		</form>
	</div>
</template>

<style>
.app-connect {
	padding: 1rem;
}
.app-connect > form {
	display: flex;
	flex-direction: column;
	max-width: 50rem;
}
.app-connect > form > label {
	margin-top: 0.5rem;
}
</style>
