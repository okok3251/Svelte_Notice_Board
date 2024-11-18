<script>
    import { link } from 'svelte-spa-router';
</script>

<nav>
    <div class="nav-container">
        <a use:link href="/" class="logo">Notice Board</a>
        <div class="nav-links">
            <a use:link class="nav-link" href="/user-create">회원가입</a>
            <a use:link class="nav-link" href="/user-login">로그인</a>
        </div>
    </div>
</nav>

<style>
    nav {
        width:90vw;
        margin : auto;
        background-color: #5C4450;
        padding: 15px 15px;
        color: white;
    }

    .nav-container {
        width: 100%;
        margin: 0 auto;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .logo {
        font-size: 24px;
        font-weight: bold;
        text-decoration: none;
        color: white;
    }

    .nav-links a {
        color: white;
        text-decoration: none;
        font-size: 16px;
        margin-left: 20px;
        font-weight: bold;
    }

    .nav-links a:hover {
        color: #DDD600;
    }

    .nav-links a:first-child {
        margin-left: 0;
    }
</style>
