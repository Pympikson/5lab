<template>
	<v-hover>
		<NuxtLink :to="`/news/${newsData.id}`" class="link">
			<v-list-item :elevation="hover ? 12 : 2" class="d-flex flex-column">
				<v-img
					:src="'/' + newsData.preview_image"
					alt=""
					max-height="250"
					width="100%"
				/>
				<div>
					<h2 class="text-decoration-underline mt-5">{{ newsData.name }}</h2>
					<p class="mt-5">
						{{ newsData.desc }}
					</p>
					<p class="mt-5">{{ newsData.date }}</p>
				</div>
			</v-list-item>
		</NuxtLink>
	</v-hover>
</template>

<script>
export default {
	props: {
		newsData: {
			type: Object,
			required: true
		}
	}
};
</script>
