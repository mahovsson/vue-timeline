<template>
	<vertical-timeline :inputData="data" :reversed="false" />
</template>

<script>
import data from '../data/data.json';
import VerticalTimeline from './VerticalTimeline.vue';

export default {
	components: { VerticalTimeline },
	data() {
		return {
			data: data,
		};
	},
};
</script>

<style scss>
h3 {
	margin: 10px 0 0;
}
ul {
	list-style-type: none;
	padding: 0;
}
li {
	display: inline-block;
	margin: 0 10px;
}
a {
	color: #42b983;
}
</style>
