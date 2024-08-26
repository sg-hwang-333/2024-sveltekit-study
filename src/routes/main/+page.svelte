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

<h1>메인 페이지</h1>

<ul>
	<li><a href="../">Home</a></li>
	<li><a href="main/info">Info</a></li>
</ul>
