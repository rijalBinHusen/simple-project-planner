<template>
	<div class="project">
		<div class="actions">
			<h3 @click="isShow = !isShow">{{ project.title }}</h3>
			<div class="icon">
				<span class="material-icons">edit</span>
				<span @click="deleteProject(project?.id)" class="material-icons">delete</span>
				<span class="material-icons">done</span>
			</div>
		</div>
		<div v-if="isShow">
			<p>{{ project.details }}</p>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				isShow: false,
				url: "http://localhost:3000/projects/"
			}
		},
		methods: {
			deleteProject(id) {
				fetch(this.url+id, { method: "DELETE" })
					.then(() => {
						this.$emit("deleteProject", id)
					})
			},
		},
		props: ["project"],
	}
</script>

<style>

	.project {
		margin: 20px auto;
		background: white;
		padding: 10px 20px;
		border-radius: 4px;
		box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
		border-left: 4px solid #e90074;
	}

	h3 {
		cursor: pointer;
	}

	.actions {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.material-icons {
		font-size: 24px;
		margin-left: 10px;
		color: #bbb;
		cursor: pointer;
	}

	.material-icons:hover {
		color: #777
	}

</style>
