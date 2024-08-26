<script>
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';
	import { isLogin } from '../stores/isLoginStore';

	// shadcn
	import { Input } from '$lib/components/ui/input';
	import { Button } from '$lib/components/ui/button';

	let email = '';
	let password = '';

	const handleLogin = async () => {
		try {
			await pb.collection('users').authWithPassword(email, password);
			isLogin.set(true);
			gotoLogin();
		} catch (error) {
			alert('');
			console.error('Error:', error);
		}
	};

	const gotoLogin = () => {
		goto('../');
	};
</script>

<div class="relative h-screen">
	<div class="relative h-full flex items-center justify-center">
		<div
			class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-full max-w-xl p-4"
		>
			<div class="text-center w-full">
				<a href="../" class="block mb-10">
					<img src="/images/logo/logo.png" alt="Logo" class="w-60 mx-auto" />
				</a>
			</div>
			<div class="text-center w-full border border-slate-200 rounded-lg p-8">
				<form on:submit={handleLogin}>
					<Input
						type="text"
						bind:value={email}
						required
						placeholder="이메일을 입력해주세요"
						class="w-full mb-3 px-5 py-8 text-lg"
					/>
					<Input
						type="password"
						bind:value={password}
						required
						placeholder="비밀번호를 입력해주세요"
						class="w-full mb-4 px-5 py-8 text-lg"
					/>
					<Button
						type="submit"
						class="w-full mt-4 bg-green-600 hover:bg-green-500 text-lg h-16 font-semibold"
						>로그인</Button
					>
				</form>
			</div>
			<div class="text-center w-full mt-4">
				<ul class="flex justify-center gap-5 text-slate-500">
					<li><a href="/">비밀번호 찾기</a></li>
					|
					<li><a href="../signup">회원가입</a></li>
				</ul>
			</div>
		</div>
	</div>
</div>
