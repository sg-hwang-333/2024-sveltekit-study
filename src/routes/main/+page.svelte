<script>
	import { goto } from '$app/navigation';

	const user = localStorage.getItem('pocketbase_auth');
	if (user == null) {
		alert('로그인 후 이용 가능합니다');
		goto('../login');
	}

	const gotoInfo = () => {
		goto('/info');
	};
</script>

<h1>메인 페이지</h1>

<ul>
	<li>Info</li>
</ul>
