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
            // Make a POST request to the server with form data
            const response = await axios.post('http://localhost:3000/tickets', {
                category,
                title,
                description,
                status,
                priority
            });

            if (response.status === 201) {
                console.log('Ticket raised successfully:', response.data);
                alert("Ticket raised successfully");
                // Clear the form fields after successful submission
                category = '';
                title = '';
                description = '';
                priority = '';
            } else {
                console.error('Failed to raise ticket:', response.data);
                alert('Failed to raise ticket. Please try again.');
            }
        } catch (error) {
            console.error('Error raising ticket:', error);
            alert('An error occurred. Please try again.');
        }
    }
</script>

<body>
    <ul>
        <li class="ticketsystem"> TICKET SUPPORT SYSTEM </li>
        <li> <button class="logout" type="button">logout</button> </li>
        <li class="username">username</li>
    </ul>
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
        <button type="submit">Create Ticket</button>
        <a href='http://localhost:5173/ticketslisting'><button type="button">Show Tickets</button></a>
    </form>
</body>

<style>
    body {
        font-family: Georgia;
        background-color: #f4f4f4;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
    }

    h1 {
        text-align: center;
        margin-left: 50px;
        margin-bottom: 20px;
        font-family: Georgia;
    }

    form {
        background: #A8A7A7;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 400px;
        font-family: Verdana, sans-serif;
        margin-left: 550px;
    }

    .form-group {
        margin-bottom: 15px;
        background: #A8A7A7;
    }

    label {
        display: block;
        margin-bottom: 5px;
        font-weight: bold;
        font-family: Verdana, sans-serif;
    }

    input[type="text"],
    textarea,
    select {
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
        margin-left: 20px;
    }

    .priority-options label {
        margin-right: 10px;
    }

    .priority-options input {
        margin-right: 5px;
    }

    button {
        background: #E8175D;
        color: #fff;
        border: none;
        padding: 10px 15px;
        border-radius: 4px;
        cursor: pointer;
        width: 100%;
        font-family: Verdana, sans-serif;
        margin: 13px 12px 12px 10px;
        margin-left: auto;
    }

    button:hover {
        background: #db1255;
    }

    .logout {
        background: #E8175D;
        color: #fff;
        border: none;
        padding: 10px 15px;
        border-radius: 4px;
        cursor: pointer;
        width: 10%;
        font-family: Verdana, sans-serif;
        margin: 13px 12px 12px 10px;
        float: right;
        margin-top: 15px;
    }

    ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
        overflow: hidden;
        background-color: #A8A7A7;
    }

    .ticketsystem {
        float: left;
        line-height: 60px;
        margin-left: 20px;
    }

    .username {
        float: right;
        line-height: 60px;
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        font-size: 20px;
    }
</style>




<!-- 
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
            console.log('Ticket Raised successfully:', response.data);
            alert("Ticket Raised successfully")
            // Clear the form fields after successful submission
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
    <ul>
        <li class="ticketsystem"> TICKET SUPPORT SYSTEM </li>
        <li> <button class="logout", type="button">logout</button> </li>
        <li class="username"> username </li>
    </ul>
<h1>Raise a Ticket </h1>

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
    <button type="submit">Create Ticket</button>
    <a href='http://localhost:5173/ticketslisting'><button type="button">Show Tickets</button></a>
</form>



</body>

<style>
    body {
        font-family: Georgia;
        background-color: #f4f4f4;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
    }

    h1 {
        text-align: center;
        margin-left: 50px;
        margin-bottom: 20px;
        font-family: Georgia;
    }

    form {
        background: #A8A7A7;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 400px;
        font-family: Verdana, sans-serif;
        margin-left: 550px;
    }

    .form-group {
        margin-bottom: 15px;
        background: #A8A7A7;
    }

    label {
        display: block;
        margin-bottom: 5px;
        font-weight: bold;
        font-family: Verdana, sans-serif;
    }

    input[type="text"],
    textarea,
    select {
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
        margin-left: 20px;
    }

    .priority-options label {
        margin-right: 10px;
    }

    .priority-options input {
        margin-right: 5px;
    }

    button {
        background: #E8175D;
        color: #fff;
        border: none;
        padding: 10px 15px;
        border-radius: 4px;
        cursor: pointer;
        width: 100%;
        font-family: Verdana, sans-serif;
        margin:13px 12px 12px 10px;
        margin-left:auto;
    }

    button:hover {
        background: #db1255;
    }

    .logout{
        background: #E8175D;
        color: #fff;
        border: none;
        padding: 10px 15px;
        border-radius: 4px;
        cursor: pointer;
        width: 10%;
        font-family: Verdana, sans-serif;
        margin:13px 12px 12px 10px;
        float:right;      
        margin-top:15px;
        
    }
    ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
        overflow: hidden;
        background-color: #A8A7A7;
        
    }
    .ticketsystem{
        float:left;
        line-height:60px;
        margin-left:20px;
    }
    .username{
        float:right;
        line-height:60px;
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        font-size: 20px;
    }
</style> -->
