<template>
	<div id="app" class="text-center">
		<h1>Word Translator</h1>
		<h5>Powered By Vue.js</h5>
		<TranslateForm v-on:formSubmit="translateText"></TranslateForm>
		<TranslateOutput v-text="translatedText"></TranslateOutput>
	</div>
</template>

<script>
import TranslateForm from './components/TranslateForm';
import TranslateOutput from './components/TranslateOutput';

export default {
	name: 'app',
	components: {
		TranslateForm,
		TranslateOutput
	},
	data: function () {
		return {
			translatedText: ""
		}
	},
	methods: {
		translateText: function (text, language) {
			this.$http.get("https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170401T223615Z.a5ee6ced4b8dc40f.a4c6f9c64be68e3d68edcc7b556adf621b7ed239&lang=" + language + "&text=" + text)
				.then((response) => {
					this.translatedText =  response.body.text[0];
				});
		}
	}
}
</script>

<style>
body {
	background: #fefefe
}
</style>
