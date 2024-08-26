<script>
	// @ts-nocheck
	import { pb } from '$lib/pocketbase';
	import { isLogin } from './stores/isLoginStore';

	import '../app.postcss';

	import { page } from '$app/stores';

	let currentPage;
	$: currentPage = $page.url.pathname;

	const handleLogout = () => {
		isLogin.set(false);
		pb.authStore.clear();
		alert('로그아웃 되었습니다');
	};
</script>

{#if !currentPage.startsWith('/signin') && !currentPage.startsWith('/signup')}
	<nav class="mx-auto max-w-screen-2xl mb-8">
		<ul class="flex justify-between items-center lg:px-32 md:px-16 px-5 py-5">
			<a href="/">
				<img src="/images/logo/logo-mini.png" alt="" class="h-24 block md:hidden" />
				<img src="/images/logo/logo.png" alt="" class="md:h-24 md:block hidden" />
			</a>
			{#if $isLogin}
				<button on:click={handleLogout} class="flex-initial">로그아웃</button>
			{:else}
				<div class="flex gap-8">
					<li><a href="/signin" class="flex-initial">로그인</a></li>
					<li><a href="/signup" class="flex-initial">회원가입</a></li>
				</div>
			{/if}
		</ul>
	</nav>
{/if}

<div class="mx-auto max-w-screen-2xl lg:px-36 md:px-20 px-8">
	<slot />
</div>
