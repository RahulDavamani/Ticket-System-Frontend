<script>
    import axios from 'axios';
    import { navigate } from 'svelte-routing';

    let firstName = '';
    let lastName = '';
    let username = '';
    let email = '';
    let password = '';

    async function register() {
        try {
            await axios.post('http://localhost:3000/register', {
                firstName,
                lastName,
                username,
                email,
                password
            });
            alert('Registration successful!');   
        } catch (error) {
            console.error('Error registering:', error);
            alert('Registration failed');
        }
    if (alert == "Registration successful!") {
        navigate('http://localhost:5173/login');
    } else {
        navigate('http://localhost:5173/register');
    }

    }
</script>

<form on:submit|preventDefault={register}>
    <h1>Register</h1>
    <label>
        First Name: 
        <input type="text" bind:value={firstName} required />
    </label>
    <label>
        Last Name:
        <input type="text" bind:value={lastName} required />
    </label>
    <label>
        Username:
        <input type="text" bind:value={username} required />
    </label>
    <label>
        Email:
        <input type="email" bind:value={email} required />
    </label>
    <label>
        Password:
        <input type="password" bind:value={password} required />
    </label>
    <button type="submit">Register</button>
    <p> Already having account? <a href="http://localhost:5173/login">Login</a></p>

</form>

<style>
    form {
        background:#A8A7A7;
        padding: 10px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 450px;
        margin-left:520px;
        margin-top: 100px;
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
