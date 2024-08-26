<script>
	// @ts-nocheck
	import { afterUpdate, onMount, tick } from 'svelte';
	import { isLogin } from '../../stores/isLoginStore';
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';

	let name = '';
	let email = '';

	onMount(async () => {
		const item = pb.authStore.model;
		if (item) {
			name = item.name;
			email = item.email;
		}
	});

	afterUpdate(() => {
		if (!$isLogin) {
			window.alert('로그인 후 사용 가능합니다');
			goto('../../login');
		}
	});
</script>

<h1>내 정보 확인하기</h1>

{#if $isLogin}
	<div>이름: {name}</div>
	<div>이메일: {email}</div>
{/if}
