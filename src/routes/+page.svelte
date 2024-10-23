<script>
	// @ts-nocheck
	import silsueRelationship from '$lib/json/silsueRelationship.js';
	import Layout from './+layout.svelte';
	const silsues = ['rodang', 'hongsam', 'candy', 'doduck', 'gom', 'light'];
	const silsuesKR = ['경로당', '홍삼', '캔디', '킹도둑', '곰준식', '빛'];
	const silsueColor = [''];

	$: isSilsueData = false;
	let silsueData = [];
	let nowSelectSilsueIdx = '';

	const showRelationship = (silsueName, index) => {
		for (const [key, value] of Object.entries(silsueRelationship)) {
			if (key == silsueName) {
				silsueData = value;
				break;
			}
		}
		nowSelectSilsueIdx = index;
		isSilsueData = true;
	};
</script>

<div class="my-10 mx-5">
	<header class="text-center">
		<div class="text-lg mb-2">~ 실수는 실수를 어떻게 생각하는가 ~</div>
		<div class="font-bold text-3xl">실수 롤링페이퍼 프로젝트</div>
	</header>

	<main class="my-20">
		<div class="flex justify-center items-center flex-wrap gap-4">
			{#each silsues as silsue, i}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
				<img
					src="/profile/{i + 1}-{silsue}.png"
					alt="silsue"
					class="w-32 h-32 object-cover rounded-full border-2 border-gray-400 cursor-pointer hover:w-36 hover:h-36 transition-all"
					on:click={() => showRelationship(silsue, i)}
				/>
			{/each}
		</div>

		<div class="mt-14 flex justify-center flex-wrap gap-x-6 gap-y-4">
			{#if isSilsueData}
				{#each silsueData as data, i}
					{#if nowSelectSilsueIdx !== i}
						<div class="max-w-[400px] h-fit bg-gray-200 px-5 py-3 rounded-lg">
							<div class="font-bold mb-3 text-lg">{i + 1} {silsuesKR[i]}</div>
							<div>
								{data}
							</div>
						</div>
					{/if}
				{/each}
			{/if}
		</div>
	</main>
</div>
