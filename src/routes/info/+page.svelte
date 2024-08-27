<script>
	// @ts-nocheck
	import { afterUpdate, onMount } from 'svelte';
	import { isLogin } from '../stores/isLoginStore';
	import { goto } from '$app/navigation';
	import { pb } from '$lib/pocketbase';

	// shadcn
	import * as Avatar from '$lib/components/ui/avatar';

	// icon
	import User from 'lucide-svelte/icons/user';
	import Pencil from 'lucide-svelte/icons/pencil';

	const gotoEdit = () => {
		goto('info/edit');
	};
</script>

<div class="text-center w-fit">
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<!-- svelte-ignore a11y-no-static-element-interactions -->
	<div class="relative hover:cursor-pointer" on:click={gotoEdit}>
		<div class="absolute border bg-white rounded-full p-2 m-2 z-10 top-28 left-28">
			<Pencil class="size-5" />
		</div>
		<Avatar.Root class="w-40 h-40 mb-4 border">
			<Avatar.Image
				src="http://127.0.0.1:8090/api/files/users/{pb.authStore.model.id}/{pb.authStore.model
					.avatar}"
				class="object-cover"
				alt="@shadcn"
			/>
			<Avatar.Fallback>
				<User class="mr-2 h-16 w-16 pl-2" />
			</Avatar.Fallback>
		</Avatar.Root>
	</div>
	<div class="font-black text-3xl mb-1">{pb.authStore.model.name}</div>
	<div class="text-slate-500">{pb.authStore.model.email}</div>
</div>
