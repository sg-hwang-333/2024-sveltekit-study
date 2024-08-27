<script>
	// @ts-nocheck
	import { pb } from '$lib/pocketbase';
	import { isLogin } from './stores/isLoginStore';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	import '../app.postcss';

	import { page } from '$app/stores';

	// shadcn
	import * as DropdownMenu from '$lib/components/ui/dropdown-menu';
	import * as Avatar from '$lib/components/ui/avatar';

	// icon
	import LogOutIcon from 'lucide-svelte/icons/log-out';
	import User from 'lucide-svelte/icons/user';

	let currentPage;
	$: {
		currentPage = $page.url.pathname;
		console.log(currentPage);
	}

	const handleLogout = () => {
		isLogin.set(false);
		pb.authStore.clear();
		alert('로그아웃 되었습니다');
	};

	const gotoInfo = () => {
		goto('/info');
	};
</script>

{#if !currentPage.startsWith('/signin') && !currentPage.startsWith('/signup')}
	<header class="mx-auto max-w-screen-2xl">
		<ul class="flex justify-between items-center lg:px-32 md:px-16 px-5 py-5">
			<a href="/">
				<img src="/images/logo/logo-mini.png" alt="" class="h-24 block md:hidden" />
				<img src="/images/logo/logo.png" alt="" class="md:h-20 md:block hidden" />
			</a>
			{#if $isLogin}
				<DropdownMenu.Root>
					<DropdownMenu.Trigger>
						{#key currentPage}
							<Avatar.Root>
								<Avatar.Image
									class="border"
									src="http://127.0.0.1:8090/api/files/users/{pb.authStore.model.id}/{pb.authStore
										.model.avatar}"
									alt="@shadcn"
								/>
								<Avatar.Fallback>
									<User class="mr-2 h-7 w-7 pl-2" />
								</Avatar.Fallback>
							</Avatar.Root>
						{/key}
					</DropdownMenu.Trigger>
					<DropdownMenu.Content>
						<DropdownMenu.Group>
							<DropdownMenu.Label>'{pb.authStore.model.name}' 님</DropdownMenu.Label>
							<DropdownMenu.Separator />
							<DropdownMenu.Item on:click={gotoInfo} class="cursor-pointer">
								<User class="mr-2 h-4 w-4" />
								<span>마이페이지</span>
							</DropdownMenu.Item>
						</DropdownMenu.Group>
						<DropdownMenu.Separator />
						<DropdownMenu.Group>
							<DropdownMenu.Item on:click={handleLogout} class="cursor-pointer">
								<LogOutIcon class="mr-2 h-4 w-4" />
								<span>로그아웃</span>
							</DropdownMenu.Item>
						</DropdownMenu.Group>
					</DropdownMenu.Content>
				</DropdownMenu.Root>
			{:else}
				<div class="flex gap-8">
					<li><a href="/signin" class="flex-initial">로그인</a></li>
					<li><a href="/signup" class="flex-initial">회원가입</a></li>
				</div>
			{/if}
		</ul>

		<nav class="border-b-2 mx-32 lg:mx-32 md:mx-16 mx-5 py-5 mb-8">
			<ul class="flex gap-14 items-center px-5">
				<li><a href="/practice">연습 페이지</a></li>
				<li><a href="/info">마이페이지</a></li>
			</ul>
		</nav>
	</header>
{/if}

<div class="mx-auto max-w-screen-2xl lg:px-36 md:px-20 px-8 mb-40">
	<slot />
</div>
