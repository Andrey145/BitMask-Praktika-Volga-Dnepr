<script>
export default {
	name: 'BitMask',
	props: {
		numBytes: {
			type: String,
			default: '1'
		},
		mask: {
			type: String,
			default: '0'
		},
		activeColor: {
			type: String,
			default: '#00ff00'
		},
		inactiveColor: {
			type: String,
			default: '#999999'
		}
	},
	computed: {
		numBits: function() {
			let number = parseInt(this.numBytes)
			if (isNaN(number))
				return 0
			return 8*number
		},
		maskDecimal: function() {
			let decimal = parseInt(this.mask)
			if (this.mask.substring(0, 2) == '0b' || this.mask.substring(0, 2) == '0B')
				decimal = parseInt(this.mask.substring(2, decimal.length), 2)
			if (this.mask.substring(0, 2) == '0o' || this.mask.substring(0, 2) == '0O')
				decimal = parseInt(this.mask.substring(2, decimal.length), 8)
			if (this.mask.substring(0, 2) == '0x' || this.mask.substring(0, 2) == '0X')
				decimal = parseInt(this.mask.substring(2, decimal.length), 16)
			return decimal
		}
	},
	methods: {
		isBitActive: function(index, maskDecimal) {
			if (maskDecimal % (Math.pow(2, index)) >= (Math.pow(2, index)) / 2)
				return true
			return false
		},
		bitColor: function(index, maskDecimal) {
			if (this.isBitActive(index, maskDecimal) == true)
				return this.activeColor
			return this.inactiveColor
		},
		valid: function(numBits, maskDecimal) {
			if (numBits <= 0 || isNaN(maskDecimal))
				return false
			return true
		}
	}
}
</script>

<template>
<div>
	<div v-show="!valid(numBits, maskDecimal)" class="invalid">Invalid mask</div>
	<div v-show="valid(numBits, maskDecimal)">
		<div class="cell" v-for="item in numBits" :key="item" v-bind:style="{'background-color': bitColor(numBits+1-item, maskDecimal)}"></div>
	</div>
</div>
</template>

<style>
.cell {
	display: inline-block;
	float: left;
	width: 7px;
	height: 12px;
	border-top: 2px solid black;
	border-bottom: 2px solid black;
	border-right: 1px solid black;
}
.cell:first-child {
	border-left: 2px solid black;
}
.cell:nth-child(8n) {
	border-right: 2px solid black;
}
.invalid {
	float: left;
}
</style>