<template>
	<div class="project-component">
		<div class="project-name lined-paper">
			<span>{{ project.name }}</span>
		</div>
		<ul class="semantic-list">
			<li class="list-item" v-for="(task, index) in tasks" :key="index">
				<Task class="project-task" :task="task"/>
			</li>
		</ul>
		<div class="lined-space lined-paper"> - </div>
	</div>
</template>

<script>
import Task from "@/components/game/Task";
import tasks from '../../tasks.json'; 

export default {
	name: 'Project',
	components: {
		Task,
	},
	props: {
		project: {
			type: Object,
			required: true,
		},
	},
	data () {
		return {
			currentTask: tasks.filter(task => task.status === 'completed').length, // calculate currentTask on initialization
			totalTasks: tasks.filter(task => task.status !== 'inactive').length, // calculate totalTasks excluding 'inactive' tasks,
			tasks: tasks
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
	.project-component {
		width: 100%;
		height: 100%;
		pointer-events: none;
		font-family: $heading-font;
	}

	.project-name {
		display: flex;
		justify-content: space-between;
		align-items: center;
		position: relative;
		width: 100%;
		height: 100%;
		padding: .5em 0;
		font-family: $heading-font;
		font-size: $font-size-xxl;
		text-transform: uppercase;

		@include desktop {
			padding: .5em 1em;
			font-size: $font-size-lg;
		}

		&:after {
			content: '';
			position: absolute;
			right: 0;
			left: 0;
			bottom: .1em;
			height: 5px;
			width: 100%;
			background-image: url('~@/assets/images/pen-underline.svg');
			background-repeat: no-repeat;
			background-size: cover;
		}
	}

	.lined-space.lined-paper {
		color: $light-primary;
		user-select: none;
	}

	.completion-percentage-component { color: $highlight-secondary; }
</style>
