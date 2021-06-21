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

</style>
