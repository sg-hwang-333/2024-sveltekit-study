<script>
	// @ts-nocheck
	import { pb } from '$lib/pocketbase';
	import { goto } from '$app/navigation';

	// shadcn
	import * as Avatar from '$lib/components/ui/avatar';
	import Button from '$lib/components/ui/button/button.svelte';
	import Input from '$lib/components/ui/input/input.svelte';

	// icon
	import User from 'lucide-svelte/icons/user';

	let imageSrc = pb.authStore.model
		? `http://127.0.0.1:8090/api/files/users/${pb.authStore.model.id}/${pb.authStore.model.avatar}`
		: '';

	let disabled = true;
	let newName = pb.authStore.model ? pb.authStore.model.name : '';
	$: {
		if (
			newName !== pb.authStore.model.name ||
			imageSrc !==
				`http://127.0.0.1:8090/api/files/users/${pb.authStore.model.id}/${
					pb.authStore.model.avatar
				}`
		) {
			disabled = false;
		} else {
			disabled = true;
		}
	}

	const handleFileChange = (event) => {
		const file = event.target.files[0];
		if (file) {
			const reader = new FileReader();
			reader.onload = (e) => {
				imageSrc = e.target.result;
			};
			reader.readAsDataURL(file);
		}
	};

	const handleUpdate = async () => {
		const formData = new FormData();
		formData.append('name', newName);

		if (document.getElementById('fileInput').files[0]) {
			formData.append('avatar', document.getElementById('fileInput').files[0]);
		} else if (imageSrc === '') {
			formData.append('avatar', '');
		}

		try {
			await pb.collection('users').update(pb.authStore.model.id, formData);
			alert('성공적으로 수정되었습니다');
			gotoInfo();
		} catch (error) {
			alert('업데이트 중 오류가 발생했습니다.');
			console.error('Error:', error);
		}
	};

	const handleRemoveImage = () => {
		imageSrc = '';
	};

	const gotoInfo = () => {
		goto('/info');
	};
</script>

<div
	class="grid grid-cols-2 border gap-y-10 p-8 sm:grid-cols-[250px_minmax(200px,_1fr)] rounded-lg"
>
	<div class="border-b-2 pl-3 font-bold">프로필 사진</div>
	<div class="border-b-2 pb-8">
		<Avatar.Root class="w-40 h-40 mb-4 border">
			<Avatar.Image src={imageSrc} class="object-cover" alt="@shadcn" />
			<input
				type="file"
				accept="image/*"
				id="fileInput"
				class="hidden"
				on:change={handleFileChange}
			/>
			<Avatar.Fallback>
				<User class="mr-2 h-16 w-16 pl-2" />
			</Avatar.Fallback>
		</Avatar.Root>

		<div class="pt-4">
			<Button
				class="bg-white text-black border 
                        border-slate-400 font-semibold hover:bg-green-600 hover:text-white hover:border-white"
				on:click={() => document.getElementById('fileInput').click()}
			>
				사진변경</Button
			>
			<Button
				on:click={handleRemoveImage}
				class="bg-white text-black border 
                        border-slate-400 font-semibold hover:bg-green-600 hover:text-white hover:border-white"
				>삭제</Button
			>
		</div>
	</div>
	<div class="self-center pl-3 font-bold">이름</div>
	<div class=""><Input class="px-3 w-fit" bind:value={newName} /></div>
</div>

<div class="mt-10 text-center">
	<Button class="bg-green-600 hover:bg-green-500" {disabled} on:click={handleUpdate}>적용</Button>
	<Button
		class="bg-white text-red-500 border border-red-500 hover:bg-red-500 hover:text-white"
		on:click={gotoInfo}>취소</Button
	>
</div>
