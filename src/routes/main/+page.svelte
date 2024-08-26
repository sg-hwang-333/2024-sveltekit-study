<script>
	import { pb } from '$lib/pocketbase';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import { isLogin } from '../stores/isLoginStore';

	onMount(() => {
		if (!isLogin) {
			alert('로그인 후 이용 가능합니다');
			goto('/login');
		}
	});
</script>

<h1>메인 페이지</h1>

<ul>
	<li><a href="../">Home</a></li>
	<li><a href="main/info">Info</a></li>
</ul>
