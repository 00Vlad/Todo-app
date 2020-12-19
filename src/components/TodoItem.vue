<template>
		<li>
			<span :class="{done: todo.completed}">
				<input type="checkbox" @change="todo.completed = !todo.completed">
				<strong>{{ index + 1 }}</strong>
				{{ todo.title | uppercase}}
			</span>
			<button class="rm" @click="$emit('remove-todo', todo.id)">
				&times;
			</button>
		</li>
</template>



<script>
export default {
	props: {
		todo: {
			type: Object,
			required: true
    },
    index: Number
	},
	computed: {
		
	},
	filters: {
		uppercase(value) {
			return value[0].toUpperCase() + value.slice(1)
		}
	}
}
</script>



<style scoped>
	li {
		display: flex;
		justify-content: space-between;

		padding: .5rem 2rem;
		margin-bottom: 1rem;

		border: 1px solid #ccc;
    cursor: pointer;
    transition: all .2s ease;
	}
  li:hover {
    background: rgb(230, 230, 230);
    padding: .8rem 2.2rem;
    font-size: 1.1rem;
  }
  li:hover input {
    visibility: visible;
  }
	input {
    visibility: hidden;
		margin-right: 1rem;
	}
  span {
    padding-top: .2em;
  }
	.rm {
		background: red;
		color: white;
    border: 2px solid red;

		font-size: 1.2rem;
		font-weight: bold;

    border-radius: 50%;
    outline: none;
		box-shadow: 0 1px 3px rgb(99, 99, 99);
    cursor: pointer;
    transition: all .3s ease;
	}
  .rm:hover {
    background: white;
    color: red;
  }
  .rm:active {
    box-shadow: 0 0 10px rgb(99, 99, 99);
  }
	.done {
		color: #ccc;
		text-decoration: line-through;
	}
</style>