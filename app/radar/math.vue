
<script>
"use strict"

class RadarMath {
	constructor(s1, s2, url, pixelWidth, pixelHeight) {
		this.url = url;
		this.pixelWidth = pixelWidth;
		this.pixelHeight = pixelHeight;

		var [Cx1, Cy1, Px1, Py1] = s1;
		var [Cx2, Cy2, Px2, Py2] = s2;

		var Rx = (Cx2 - Cx1) / (Px2 - Px1);
		var Ry = (Cy2 - Cy1) / (Py2 - Py1);

		this.originLeft = Cx1 - (Cx2 - Cx1) * Px1 / (Px2 - Px1);
		this.originRight = Cx2 + (pixelWidth - Px2) * Rx;
		this.originTop = Cy1 - Py1 * Ry;
		this.originBottom = Cy2 + (pixelHeight - Py2) * Ry;
		this.originWidth = this.originRight - this.originLeft;
		this.originHeight = this.originBottom - this.originTop;
	}
	toPixel(origin) {
		let x = (origin[0] - this.originLeft) * this.pixelWidth / this.originWidth;
		let y = (origin[1] - this.originTop) * this.pixelHeight / this.originHeight;
		return [x, y];
	}
	circleToPixel(origin, radius) {
		let x = (origin[0] - this.originLeft) * this.pixelWidth / this.originWidth;
		let y = (origin[1] - this.originTop) * this.pixelHeight / this.originHeight;
		let r = radius * this.pixelWidth / this.originWidth;
		return [x, y, r];
	}
}
</script>
