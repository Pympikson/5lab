<template>
	<v-row>
		<v-list class="d-flex flex-column">
			<Article v-for="news in newsList" :key="news.id" :newsData="news" />
		</v-list>
	</v-row>
</template>

<script>
import { mapState } from "vuex";

export default {
	computed: {
		...mapState("news", ["newsList"])
	}
};
</script>

<style lang="scss">
.on-hover {
	cursor: pointer;
	transform: scale(1.003);
	transition: 200ms;
}

.link {
	text-decoration: none;
}
</style>
