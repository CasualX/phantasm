
<script>
"use strict"

class WebSocketStore {
	constructor() {
		this.address = 'ws://localhost:30145/';
		this.username = 'Anonymous';
		this.secret = '';

		this.socket = null;
		this.error = null;

		this.game = null;
		this.state = null;
		this.role = null;
		this.paused = false;
		this.debugText = "";
	}
	reset() {
		if (this.socket) {
			this.socket.onopen = null;
			this.socket.onclose = null;
			this.socket.onerror = null;
			this.socket.onmessage = null;
			this.socket = null;
		}
		this.game = null;
		this.state = null;
		this.role = null;
		this.paused = false;
		this.debugText = "";
	}
	connect() {
		this.error = null;
		try {
			let sock = new WebSocket(this.address);
			sock.onopen = event => this.onopen(event);
			sock.onclose = event => this.onclose(event);
			sock.onerror = event => this.onerror(event);
			sock.onmessage = event => this.onmessage(event);
			this.socket = sock;
		}
		catch (ex) {
			console.error(ex);
			this.error = ex;
		}
	}
	disconnect() {
		if (this.socket) {
			this.socket.close();
		}
	}
	connected() {
		return this.socket != null && this.role != null;
	}
	onopen(event) {
		this.socket.send("net.login! " + this.username);
	}
	onclose(event) {
		this.reset();
	}
	onerror(event) {
		this.reset();
		this.error = `Can't establish a connection to the server at ${this.address}.`;
		console.error(event);
	}
	onmessage(event) {
		try {
			let data = JSON.parse(event.data);
			switch (data.target) {
				case 'auth/welcome':
					this.welcome(data.message);
					break;
				case 'attachGame':
					this.attachGame(data.message);
					break;
				case 'detachGame':
					this.detachGame(data.message);
					break;
				case 'debug/write':
					this.debugWrite(data.message);
					break;
				case 'console/log':
					console.log(data.message);
					break;
				case this.game + '/update':
					this.updateGame(data.message);
					break;
			}
		}
		catch (ex) {
			console.error(ex);
		}
	}
	welcome(role) {
		this.role = window.role = Object.freeze(role);
		console.log("Welcome " + role.name + " (" + role.addr + "): " + role.role);
	}
	attachGame(game) {
		this.game = game;
		this.socket.send("net.state!");
	}
	detachGame(game) {
		this.game = null;
	}
	updateGame(state) {
		if (!this.paused) {
			if (this.game == "apex") {
				let lookup = [];
				for (let entity of state.entity_list.entities) {
					lookup[entity.index] = entity;
				}
				state.entity_list.lookup = lookup;
			}
			else if (this.game == "mw") {
				let lookup = [];
				for (let entity of state.entities_data.list) {
					lookup[entity.index] = entity;
				}
				state.entities_data.lookup = lookup;
			}
			this.state = window.state = Object.freeze(state);
		}
		// Queue a new state request as soon as we receive one!
		if (this.game) {
			this.socket.send("net.state!");
		}
	}
	debugWrite(content) {
		if (!this.paused) {
			this.debugText = "" + content;
		}
	}
};
</script>
