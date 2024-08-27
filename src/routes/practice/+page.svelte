<script>
	import { afterUpdate } from 'svelte';
	import { goto } from '$app/navigation';
	import { isLogin } from '../stores/isLoginStore';

	afterUpdate(() => {
		if (!$isLogin) {
			window.alert('로그인 후 사용 가능합니다');
			goto('../signin');
		}
	});
</script>

<h1>연습 페이지</h1>
