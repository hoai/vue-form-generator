<template lang="pug">
	label
		input(:id="getFieldID(schema)", type="checkbox", v-model="value", :autocomplete="schema.autocomplete", :disabled="disabled", :name="schema.inputName", :class="schema.fieldClasses", v-attributes="'input'", v-on="listeners")
		&nbsp; span.name {{schema.checkboxLabel}}
</template>

<script>
import abstractField from "../abstractField";

export default {
	mixins: [abstractField]
};
</script>

<style lang="scss">
.vue-form-generator .field-checkbox input {
	margin-left: 12px;
}
</style>
