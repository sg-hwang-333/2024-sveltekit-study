<script>
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';
	import { isLogin } from '../stores/isLoginStore';

	let email = '';
	let password = '';

	const handleLogin = async () => {
		isLogin.set(true);
		try {
			await pb.collection('users').authWithPassword(email, password);

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

<h1>로그인</h1>

<form on:submit={handleLogin}>
	<label>
		이메일
		<input type="text" bind:value={email} required />
	</label>

	<br /><br />

	<label>
		비밀번호
		<input type="password" bind:value={password} required />
	</label>

	<br /><br />

	<button type="submit">로그인</button>
</form>
