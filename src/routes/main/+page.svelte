<script>
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';
	import { onMount } from 'svelte';

	onMount(() => {
		const user = pb.authStore.model;
		console.log(user);
		if (user == null) {
			alert('로그인 후 이용 가능합니다');
			goto('../login');
		}
	});

	const gotoInfo = () => {
		goto('/main/info');
	};
</script>

<h1>메인 페이지</h1>

<ul>
	<button on:click={gotoInfo}>Info</button>
</ul>
