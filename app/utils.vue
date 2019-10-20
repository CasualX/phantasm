
<script>
"use strict"

/// Parse arguments from URL hash.
function argv(hash) {
	if (hash == null) {
		hash = window.location.hash;
	}
	let args = {};
	if (hash.startsWith("#")) {
		for (let arg of hash.substring(1).split("&")) {
			let [key, value] = arg.split("=");
			try {
				key = decodeURIComponent(key);
				args[key] = decodeURIComponent(value);
			}
			catch (ex) {
				console.error(ex, key, value);
			}
		}
	}
	return args;
}
</script>

<style>
.text-stroke--outline {
	text-shadow: 2px 0 0 #000, 0 -2px 0 #000, 0 2px 0 #000, -2px 0 0 #000;
}
.user-select--none {
	user-select: none;
	-moz-user-select: none;
	-webkit-user-select: none;
	-ms-user-select: none;
}
</style>
