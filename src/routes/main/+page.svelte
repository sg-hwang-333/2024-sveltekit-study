<script>
	import { pb } from '$lib/pocketbase';
	import { onMount } from 'svelte';

	onMount(() => {
		const user = pb.authStore.model;
		console.log(user);
		if (user == null) {
			alert('로그인 후 이용 가능합니다');
		}
	});
</script>

<h1>메인 페이지</h1>

<ul>
	<li><a href="../">Home</a></li>
	<li><a href="main/info">Info</a></li>
</ul>
