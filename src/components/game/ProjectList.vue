<template>
	<div :class="['project-list-component', 'list-styles']">
		<div class="project-list-header">
			<h1 class="lined-paper project-header">Projects</h1>
			<div class="task-tracker lined-paper">
				<span>{{ completedProjects }}</span> of <span>{{ totalProjects }}</span> projects completed
			</div>
			<div class="lined-space lined-paper show-desktop"> - </div>
		</div>
		<ul class="semantic-list">
			<li class="list-item" v-for="(project, index) in projects" :key="index">
				<Project :project="project"/>
			</li>
		</ul>
		<div class="lined-paper-filler"></div>
	</div>
</template>



<script>
import Project from "@/components/game/Project";
import projects from '../../projects.json'; 


export default {
	name: 'ProjectList',
	components: {
		Project,
	},
	data () {
		return {
			completedProjects: projects.filter(project => project.status === 'completed').length, 
			totalProjects: projects.filter(project => project.status !== 'inactive').length,
			projects: projects
		}
	},
	methods: {
		updateStatus(index, newStatus) {
			this.$set(this.tasks, index, { ...this.tasks[index], status: newStatus });
			this.updateTaskCount();
		},
		updateTaskCount() {
			this.currentTask = this.tasks.filter(task => task.status === 'completed').length;
		}
	}
};
</script>



<style lang="scss" scoped>
	.project-list-header {
		position: relative;
		font-family: $heading-font;
		text-transform: uppercase;
		text-align: center;
		
		@include desktop {
			.lined-paper:first-child {
				&:after {
					content: '';
					position: absolute;
					left: 25px;
					top: 0;
					bottom: 0;
					margin: auto;
					background-image: url('~@/assets/images/project-sticker.png');
					background-repeat: no-repeat;
					background-size: contain;
					background-position: center;
					width: 100px;
					height: 100px;
				}
			}
		}

		.project-header {
			display: none;
			margin: 0;

			@include desktop { display: block; }
		}
	}

	.task-tracker {
		font-size: $font-size-xxl;

		@include desktop { font-size: $font-size-lg; }

		span { color: $highlight-primary; }
	}
</style>
