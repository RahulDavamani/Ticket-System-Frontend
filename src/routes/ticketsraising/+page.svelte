<script>
    import { onMount } from 'svelte';
    import axios from 'axios';

    let category = '';
    let title = '';
    let description = '';
    let priority = '';
    let status = 'Open';

    // Function to create a new ticket
    async function createTicket() {
        try {
            const response = await axios.post('http://localhost:3000/tickets', {
                category,
                title,
                description,
                status,
                priority
            });
            console.log('Ticket raised successfully:', response.data);
            
            category = '';
            title = '';
            description = '';
            priority = '';
        } catch (error) {
            console.error('Error raising ticket:', error);
        }
    }
</script>
<body>
<h1>Raise a Ticket</h1>

<form on:submit|preventDefault={createTicket}>
    <div class="form-group">
        <label for="category">Category</label>
        <select id="category" bind:value={category} required>
            <option value="" disabled selected>Select a category</option>
            <option value="Bug">Bug</option>
            <option value="Feature Request">Feature Request</option>
            <option value="Support">Support</option>
            <option value="Payment">Payment</option>
            <option value="Others">Others</option>
        </select>
    </div>
    <div class="form-group">
        <label for="title">Title</label>
        <input type="text" id="title" bind:value={title} required />
    </div>
    <div class="form-group">
        <label for="description">Description</label>
        <textarea id="description" bind:value={description} required></textarea>
    </div>
    <div class="form-group">
        <label for="priority">Priority</label>
        <div class="priority-options">
            <input type="radio" id="low" name="priority" value="Low" bind:group={priority}>
            <label for="low">Low</label>
            <input type="radio" id="medium" name="priority" value="Medium" bind:group={priority}>
            <label for="medium">Medium</label>
            <input type="radio" id="high" name="priority" value="High" bind:group={priority}>
            <label for="high">High</label>
        </div>
    </div>
    <a href="J:\0 ticket system\ticket system 2\ticket_system_frontend\src\routes\ticketslisting\+page.svelte"><button type="submit">Create Ticket</button></a>
</form>
</body>
<style>
    body {
        background-color:#363636;
        font-family: Georgia;
    }
    h1 {
        color: #E5EAF5;
        text-align: center;
        margin-bottom: 20px;
        font-family: Georgia;
    }

    form {
        background:#A8A7A7;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 400px;
        margin-left:500px;
        font-family: Verdana,(sans-serif);
    }

    .form-group {
        margin-bottom: 15px;
    }

    label {
        background:#A8A7A7;
        display: block;
        margin-bottom: 5px;
        font-weight: bold;
        font-family: Verdana,(sans-serif);
    }

    input[type="text"],
    textarea,
    select {
        background:#ffffffcc;
        width: 100%;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 4px;
        box-sizing: border-box;
        font-family: Georgia;
    }

    textarea {
        resize: vertical;
        height: 100px;
        
    }

    .priority-options {
        display: flex;
        margin-left:20px;
    }

    .priority-options label {
        margin-right: 10px;
    }

    .priority-options input {
        margin-right: 5px;
    }

    button {
        background:#E8175D;
        color: #fff;
        border: none;
        padding: 10px 15px;
        border-radius: 4px;
        cursor: pointer;
        width: 100%;
        font-family: Verdana,(sans-serif);
    }

    button:hover {
        background:#db1255;
    }
</style>
