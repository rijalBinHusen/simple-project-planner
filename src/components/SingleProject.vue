<template>
	<div class="project" :class="{ complete: project.complete }">
		<div class="actions">
			<h3 @click="isShow = !isShow">{{ project.title }}</h3>
			<div class="icon">
				<span class="material-icons">edit</span>
				<span @click="deleteProject" class="material-icons">delete</span>
				<span @click="toggleComplete" class="material-icons tick">done</span>
			</div>
		</div>
		<div v-if="isShow">
			<p>{{ project.details }}</p>
		</div>
	</div>
</template>

<script>
/* eslint-disable */ 
	export default {
		data() {
			return {
				isShow: false,
				url: "http://localhost:3000/projects/" + this.project.id
			}
		},
		methods: {
			deleteProject() {
				fetch(this.url, { method: "DELETE" })
					.then(() => {
						this.$emit("deleteProject",  this.project.id)
					})
			},
			toggleComplete() {
				fetch(this.url, { 
					method: "PATCH",
					headers: { 'Content-Type': 'application/json'},
					body: JSON.stringify({ complete: !this.project.complete })
				}).then(() => {
					this.$emit("completeProject", this.project.id)
				}).catch((err) => {
					console.log(err)
				})
			}
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
	.project.complete {
		border-left: 4px solid #00ce89;
	}

	.project.complete .tick{
		color: #00ce89;
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
