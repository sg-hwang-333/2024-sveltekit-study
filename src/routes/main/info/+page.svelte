<script>
	// @ts-nocheck

	import { onMount } from 'svelte';

	let name = '';
	let email = '';

	onMount(() => {
		const item = JSON.parse(localStorage.getItem('pocketbase_auth')).model;
		name = item.name;
		email = item.email;
	});
</script>

<h1>내 정보 확인하기</h1>

<div>이름: {name}</div>
<div>이메일: {email}</div>
