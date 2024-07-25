<script>
    export let username = '';
</script>

<nav>
    <div class="navbar">
        <div class="navbar-brand">Ticket System</div>
        <div class="navbar-links">
            <a href="#/ticket-listing">Ticket Listing</a>
            <a href="#/ticket-raising">Raise a Ticket</a>
        </div>
        {#if username}
            <div class="navbar-user">Logged in as: {username}</div>
        {/if}
    </div>
</nav>

<style>
    nav {
        width: 100%;
        background-color: #333;
        color: white;
        padding: 10px;
    }

    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .navbar-brand {
        font-size: 24px;
    }

    .navbar-links a {
        margin: 0 10px;
        color: white;
        text-decoration: none;
    }

    .navbar-user {
        font-size: 14px;
    }
</style>
