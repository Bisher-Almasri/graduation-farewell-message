<script lang="ts">
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';

	let sections: HTMLElement[] = [];
	const visible = writable(new Set<number>());

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					const index = sections.indexOf(entry.target as HTMLElement);
					visible.update(set => {
						if (entry.isIntersecting) {
							set.add(index);
						} else {
							set.delete(index);
						}
						return set;
					});
				});
			},
			{
				root: null,
				rootMargin: '-10% 0px -10% 0px',
				threshold: 0.1
			}
		);

		sections.forEach((section) => {
			observer.observe(section);
		});

		return () => {
			sections.forEach((section) => {
				observer.unobserve(section);
			});
		};
	});
</script>

<div class="min-h-screen bg-gradient-to-b from-blue-900 to-indigo-950 text-white">
	<!-- Hero Section -->
	<section
		class="flex min-h-screen flex-col items-center justify-center px-4 text-center"
		bind:this={sections[0]}
		class:animate-fade-in={$visible.has(0)}
	>
		<div class="space-y-6">
			<h1 class="text-5xl font-bold tracking-tight sm:text-7xl">
				<span class="block text-blue-300">Farewell</span>
				<span class="mt-2 block">Grade 8</span>
			</h1>
			<div class="mt-8 animate-bounce">
				<svg
					class="mx-auto h-10 w-10 text-blue-300"
					fill="none"
					stroke="currentColor"
					viewBox="0 0 24 24"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M19 14l-7 7m0 0l-7-7m7 7V3"
					></path>
				</svg>
			</div>
		</div>
	</section>

	<!-- Teachers Section -->
	<section
		class="flex min-h-screen flex-col items-center justify-center px-4 py-16"
		bind:this={sections[2]}
		class:animate-slide-in-left={$visible.has(2)}
	>
		<div class="mx-auto max-w-4xl">
			<h2 class="mb-12 text-center text-4xl font-bold text-blue-300 sm:text-5xl">My Teachers</h2>
			<div class="grid gap-6 sm:grid-cols-2">
				<div class="rounded-xl bg-indigo-900/50 p-6 shadow-xl transition-all hover:scale-105">
					<h3 class="mb-2 text-2xl font-semibold text-blue-200">Mrs. Cooper</h3>
					<p class="text-lg font-medium text-blue-300">Homeroom Teacher</p>
					<p class="mt-4 text-lg">
						Thank you so much for being a amazing teacher, I always had fun in class,
                        and this was definitely the best year in middle school.
					</p>
				</div>
				<div class="rounded-xl bg-indigo-900/50 p-6 shadow-xl transition-all hover:scale-105">
					<h3 class="mb-2 text-2xl font-semibold text-blue-200">Mr. Cooper</h3>
					<p class="text-lg font-medium text-blue-300">English Teacher</p>
					<p class="mt-4 text-lg">
						Thank you for always finding a creative way to teach, I had so many fun 
                        and notable times in class
					</p>
				</div>
				<div class="rounded-xl bg-indigo-900/50 p-6 shadow-xl transition-all hover:scale-105">
					<h3 class="mb-2 text-2xl font-semibold text-blue-200">Mr. Doiu</h3>
					<p class="text-lg font-medium text-blue-300">French Teacher</p>
					<p class="mt-4 text-lg">
                        Merci d'avoir toujours été si encourageante et de nous avoir aidés à apprendre le français de façon amusante,
                        J'ai passé trois années formidables en français avec vous. Merci.
                        
                        
					</p>
				</div>
				<div class="rounded-xl bg-indigo-900/50 p-6 shadow-xl transition-all hover:scale-105">
					<h3 class="mb-2 text-2xl font-semibold text-blue-200">Mr. Dickson</h3>
					<p class="text-lg font-medium text-blue-300">Music Teacher</p>
					<p class="mt-4 text-lg">
						Lastly, thank you for another amazing 3 years of music, you always tought has
						music in a entertaining way, Thank you.
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- Farewell Message -->
	<section
		class="flex min-h-screen flex-col items-center justify-center px-4 py-16"
		bind:this={sections[3]}
		class:animate-fade-in={$visible.has(3)}
	>
		<div class="mx-auto max-w-3xl text-center">
			<h2 class="mb-8 text-4xl font-bold text-blue-300 sm:text-5xl">Farewell Message</h2>
			<div class="rounded-xl bg-gradient-to-r from-blue-800 to-indigo-800 p-8 shadow-2xl">
				<p class="text-xl leading-relaxed">
					Thank you so much to all of my teachers for the amazing time in class,
					I always had fun learning in class and this was definitely the best year
					in my academic life. I'm very grateful for the amazing teachrs I had,
                    thank you.
				</p>
				<p class="mt-6 text-2xl font-bold text-blue-200">- Bisher Al Masri</p>
			</div>
			
		</div>
	</section>
</div>

<style>
	@keyframes fadeIn {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	@keyframes slideInRight {
		from {
			transform: translateX(50px);
			opacity: 0;
		}
		to {
			transform: translateX(0);
			opacity: 1;
		}
	}

	@keyframes slideInLeft {
		from {
			transform: translateX(-50px);
			opacity: 0;
		}
		to {
			transform: translateX(0);
			opacity: 1;
		}
	}

	.animate-fade-in {
		animation: fadeIn 1s ease-out forwards;
	}

	.animate-slide-in-right {
		animation: slideInRight 1s ease-out forwards;
	}

	.animate-slide-in-left {
		animation: slideInLeft 1s ease-out forwards;
	}
</style>