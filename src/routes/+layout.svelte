<script>
	// @ts-nocheck
	import { pb } from '$lib/pocketbase';
	import { onDestroy, onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import { isLogin } from './stores/isLoginStore';

	import '../app.postcss';

	const handleLogout = () => {
		isLogin.set(false);
		pb.authStore.clear();
		alert('로그아웃 되었습니다');
	};
</script>

<nav>
	<ul>
		{#if $isLogin}
			<button on:click={handleLogout}>로그아웃</button>

			<main>
				<a href="/main">메인페이지</a>
			</main>
		{:else}
			<li><a href="/login">로그인</a></li>
			<li><a href="/signup">회원가입</a></li>
		{/if}
	</ul>
</nav>

<slot></slot>
