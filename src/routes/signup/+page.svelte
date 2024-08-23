<script>
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';

	let name = '';
	let email = '';
	let password = '';
	let passwordConfirm = '';

	// @ts-ignore
	const handleSubmit = async (event) => {
		try {
			// @ts-ignore
			await pb.collection('users').create({
				name: name,
				email: email,
				password: password,
				passwordConfirm: passwordConfirm
			});

			alert('유저 정보가 추가되었습니다.');
			gotoLogin();
		} catch (error) {
			console.error('Error:', error);
			alert(error);
		}
	};

	const gotoLogin = () => {
		goto('/login');
	};
</script>

<h1>회원가입</h1>

<form on:submit={handleSubmit}>
	<label>
		이름
		<input type="text" bind:value={name} required />
	</label>

	<br /><br />

	<label>
		이메일
		<input type="email" bind:value={email} required />
	</label>

	<br /><br />

	<label>
		비밀번호
		<input type="password" bind:value={password} required />
	</label>

	<br /><br />

	<label>
		비밀번호 확인
		<input type="password" bind:value={passwordConfirm} required />
	</label>

	<br /><br />

	<button type="submit">가입하기</button>
</form>
