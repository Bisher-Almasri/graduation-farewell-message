<script lang="ts">
	import { dev } from '$app/environment';
	import { inject } from '@vercel/analytics';
	inject({ mode: dev ? 'development' : 'production' });
	import '../app.css';

	let { children } = $props();
</script>

{@render children()}
