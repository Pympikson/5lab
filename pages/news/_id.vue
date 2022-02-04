<template>
	<v-row class="d-flex flex-column">
		<v-img
			:src="'/' + newsData.full_image"
			alt=""
			max-height="250"
			width="100%"
		/>
		<div class="wrapper d-flex flex-column ma-10">
			<h1 class="display-2 mb-10">{{ newsData.name }}</h1>
			<p>{{ newsData.desc }}</p>
			<p class="font-weight-light">{{ newsData.date }}</p>

			<v-row>
				<v-col>
					<v-text-field
						v-model="user_name"
						label="Ваше имя"
						required
					></v-text-field>

					<v-text-field
						v-model="comment"
						label="Ваш комментарий"
						required
					></v-text-field>
					<v-btn
						:disabled="submitDisabled"
						class="mt-5 mb-10"
						@click="onSubmitClick"
					>
						Добавить комментарий
					</v-btn>
				</v-col>
			</v-row>

			<v-card
				class="pa-4 my-2 col comment"
				v-for="comment in comments"
				:key="comment.id"
			>
				<div class="comment__text">
					{{ comment.comment }}
				</div>

				<div class="font-italic">{{ comment.user_name }}</div>
			</v-card>
		</div>
	</v-row>
</template>

<script>
import { mapState } from "vuex";

export default {
	data: () => ({
		newsData: "",
		comments: [],
		user_name: "",
		comment: "",
		submitDisabled: false
	}),
	async asyncData({ params }) {
		const id = params.id;
		return { id };
	},
	computed: { ...mapState("news", ["newsList"]) },
	async mounted() {
		this.newsData = this.newsList.find(e => e.id == this.id);
		this.comments = await this.$store.dispatch(
			"news/getArticleComments",
			this.id
		);
	},
	methods: {
		async onSubmitClick() {
			this.submitDisabled = true;
			await this.$store.dispatch("news/addArticleComment", {
				id: this.id,
				user_name: this.user_name,
				comment: this.comment
			});

			this.comments = await this.$store.dispatch(
				"news/getArticleComments",
				this.id
			);

			this.comment = "";
			this.user_name = "";
			this.submitDisabled = false;
		}
	}
};
</script>
