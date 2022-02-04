<template>
	<v-carousel height="100vh">
		<v-carousel-item
			v-for="article in sliderNews"
			:key="article.id"
			:src="`/${article.full_image}`"
		/>
	</v-carousel>
</template>
<script>
import { mapState } from "vuex";

export default {
	computed: {
		...mapState("news", ["newsList"]),
		sliderNews() {
			return this.newsList.filter(article => article.slider);
		}
	}
};
</script>
