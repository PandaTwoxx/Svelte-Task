<script lang="ts">
	import '../app.css'
	let { title, description } = $props()
</script>
<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{title}</h5>
<p class="mb-3 font-normal text-gray-700 dark:text-slate-400">{description}</p>
