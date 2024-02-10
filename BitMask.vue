<script>
export default {
	name: 'BitMask',
	props: {
		mask: String,
		activeColor: String,
		inactiveColor: String
	},
	methods: {
		bitColor: function(index) {
			let maskDecimal = parseInt(this.mask)
			if (this.mask.substring(0, 2) == '0b' | this.mask.substring(0, 2) == '0B')
				maskDecimal = parseInt(this.mask.substring(2, maskDecimal.length), 2)
			if (this.mask.substring(0, 2) == '0o' | this.mask.substring(0, 2) == '0O')
				maskDecimal = parseInt(this.mask.substring(2, maskDecimal.length), 8)
			if (this.mask.substring(0, 2) == '0x' | this.mask.substring(0, 2) == '0X')
				maskDecimal = parseInt(this.mask.substring(2, maskDecimal.length), 16)
			if (maskDecimal % (Math.pow(2, index)) >= (Math.pow(2, index)) / 2)
				return this.activeColor
			return this.inactiveColor
		}
	}
}
</script>

<template>
<div className="square" v-bind:style="{'background-color': bitColor(16)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(15)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(14)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(13)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(12)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(11)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(10)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(9)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(8)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(7)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(6)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(5)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(4)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(3)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(2)}"></div>
<div className="square" v-bind:style="{'background-color': bitColor(1)}"></div>
<div className="squareEnd"></div>
</template>

<style>
.square {
	display: inline-block;
	float: left;
	width: 7px;
	height: 10px;
	border-top: 2px solid black;
	border-bottom: 2px solid black;
	border-left: 2px solid black;
}
.squareEnd {
	display: inline-block;
	float: left;
	height: 12px;
	border: 1px solid black;
}
</style>