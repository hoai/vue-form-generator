<template lang="pug">
	input.form-control(type="text", v-model="value", :autocomplete="schema.autocomplete", :disabled="disabled", :placeholder="schema.placeholder", :readonly="schema.readonly", :name="schema.inputName", :id="getFieldID(schema)", v-on="listeners")
</template>

<script>
/* global $ */
import abstractField from "../abstractField";

export default {
	mixins: [abstractField],
	computed: {
		maskOptions() {
			let frm = this;
			let opts = {
				onComplete: function (cep) {
					frm.updateValue(cep);
				},
				onChange: function (val) {
					frm.updateValue(val);
				}
			};
			return this.schema.maskOptions || opts;
		}
	},
	mounted() {
		this.$nextTick(function () {
			if (window.$ && window.$.fn.mask) {
				$(this.$el)
					.unmask()
					.mask(this.schema.mask, this.maskOptions);
			} else {
				console.warn(
					"JQuery MaskedInput library is missing. Please download from https://github.com/digitalBush/jquery.maskedinput and load the script in the HTML head section!"
				);
			}
		});
	},

	beforeDestroy() {
		if (window.$ && window.$.fn.mask) $(this.$el).unmask();
	},
	methods: {
		updateValue(newValue) {
			this.value = newValue;
		}
	}
};
</script>

<style lang="scss">

</style>
