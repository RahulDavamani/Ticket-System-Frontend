<script>
    import axios from 'axios';
    import { navigate } from 'svelte-routing';
    import { writable } from 'svelte/store';
    import page from 'J:\\0 ticket system\\ticket system 2\\ticket_system_frontend\\src\\routes\\ticketsraising\\+page.svelte';

    export const user = writable(null);
    let username = '';
    let password = '';

    async function login() {
        try {
            const response = await axios.post('http://localhost:3000/login', { username, password });
            localStorage.setItem('token', response.data.token);
            user.set(response.data.user);
            alert('Login successful!');
            navigate('/ticketsraising');
        } catch (error) {
            console.error('Error logging in:', error);
            alert('Login failed');
        }
    }
</script>
<body>
<form on:submit|preventDefault={login}>
    <h1>Login</h1>

    <label for="username">
        Username:
        <input type="text" bind:value={username} required /><br>
    </label>
    <label>
        Password:
        <input type="password" bind:value={password} required /><br>
    </label>
    <button type="submit">Login</button>
    <p> new user? <a href="http://localhost:5173/register">Register</a></p>

</form>
</body>
<style>
    body {
        background-color: #f5f5f5;
    }
    form {
        background:#A8A7A7;
        padding: 10px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 350px;
        margin-left:550px;
        margin-top: 200px;
        font-family: Verdana,(sans-serif);
        text-align:center;
        
    }

    label {
        flex-direction: column;
        width: 100%;
        padding: 12px 20px;
        margin: 8px 0;
        display: inline-block;
        border: 1px;
        box-sizing: border-box;
        
    }

    button {
        background: #c62774;
        color: white;
        border: none;
        padding: 0.5rem 1rem;
        cursor: pointer;
    }

    button:hover {
        background: #b43371;
    }
</style>
