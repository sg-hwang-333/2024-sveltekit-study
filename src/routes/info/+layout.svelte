<script>
	// @ts-nocheck
	import { afterUpdate, onMount } from 'svelte';
	import { isLogin } from '../stores/isLoginStore';
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';

	onMount(async () => {
		console.log(pb.authStore.model);
	});

	afterUpdate(() => {
		if (!$isLogin) {
			window.alert('로그인 후 사용 가능합니다');
			goto('../../signin');
		}
	});
</script>

<div class="mb-16">
	<div class="text-2xl font-bold mb-1">마이페이지</div>
	<span class="text-base">프로필을 확인 및 수정하실 수 있습니다.</span>
</div>

{#if $isLogin}
	<slot />
{/if}
