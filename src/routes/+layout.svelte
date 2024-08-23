<script>
	// @ts-nocheck
	import { pb } from '$lib/pocketbase';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	let user = false;
	onMount(() => {
		user = pb.authStore.model;
		console.log(user);
	});

	const logout = () => {
		pb.authStore.clear();
		alert('로그아웃 되었습니다');
		location.reload();
	};
</script>

<nav>
	<ul>
		{#if user == null}
			<li><a href="/login">로그인</a></li>
			<li><a href="/signup">회원가입</a></li>
		{:else}
			<button on:click={logout}>로그아웃</button>

			<main>
				<a href="/main">메인페이지</a>
			</main>
		{/if}
	</ul>
</nav>

<slot></slot>
