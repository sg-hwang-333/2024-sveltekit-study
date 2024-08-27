<script>
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';

	// shadcn
	import { Input } from '$lib/components/ui/input';
	import { Button } from '$lib/components/ui/button';

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

			alert('회원가입이 성공적으로 완료되었습니다.');
			gotoLogin();
		} catch (error) {
			console.error('Error:', error);
			alert(error);
		}
	};

	const gotoLogin = () => {
		goto('/signin');
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
				<form on:submit={handleSubmit}>
					<Input
						type="text"
						bind:value={name}
						required
						placeholder="이름을 입력해주세요"
						class="w-full mb-3 px-5 py-8 pl-12 text-lg bg-[url('/images/icon/user/default.svg')] bg-no-repeat bg-[left_14px_center]"
					/>
					<Input
						type="email"
						bind:value={email}
						required
						placeholder="이메일을 입력해주세요"
						class="w-full mb-3 px-5 py-8 pl-12 text-lg bg-[url('/images/icon/email/default.svg')] bg-no-repeat bg-[left_14px_center]"
					/>
					<Input
						type="password"
						bind:value={password}
						required
						placeholder="패스워드를 입력해주세요"
						class="w-full mb-3 px-5 py-8 pl-12 text-lg bg-[url('/images/icon/password/default.svg')] bg-no-repeat bg-[left_14px_center]"
					/>
					<Input
						type="password"
						bind:value={passwordConfirm}
						required
						placeholder="패스워드를 다시 입력해주세요"
						class="w-full mb-3 px-5 py-8 pl-12 text-lg bg-[url('/images/icon/password/default.svg')] bg-no-repeat bg-[left_14px_center]"
					/>
					<Button
						type="submit"
						class="w-full mt-4 bg-green-600 hover:bg-green-500 text-lg h-16 font-semibold"
						>회원가입</Button
					>
				</form>
			</div>
		</div>
	</div>
</div>
