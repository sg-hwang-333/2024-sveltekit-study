<script>
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';
	import { isLogin } from '../stores/isLoginStore';

	import { Input } from '$lib/components/ui/input';

	let email = '';
	let password = '';

	const handleLogin = async () => {
		try {
			await pb.collection('users').authWithPassword(email, password);
			isLogin.set(true);
			alert('로그인 성공');
			gotoLogin();
		} catch (error) {
			alert('로그인 실패');
			console.error('Error:', error);
		}
	};

	const gotoLogin = () => {
		goto('../');
	};
</script>

<h1 class="text-3xl font-bold underline">로그인</h1>

<form on:submit={handleLogin}>
	<!-- svelte-ignore a11y-label-has-associated-control -->
	<label>
		이메일
		<Input type="text" bind:value={email} required />
	</label>

	<br /><br />

	<!-- svelte-ignore a11y-label-has-associated-control -->
	<label>
		비밀번호
		<Input type="password" bind:value={password} required />
	</label>

	<br /><br />

	<button type="submit">로그인</button>
</form>
