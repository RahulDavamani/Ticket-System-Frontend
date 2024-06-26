<script>
    import { onMount } from 'svelte';
    import axios from 'axios';

    let tickets = [];
    let categories = ['Bug', 'Feature Request', 'Support','Payment','Others']; 
    let selectedCategory = '';

    // Function to fetch tickets from backend
    async function fetchTickets(category = '') {
        try {
            const response = await axios.get('http://localhost:3000/tickets', {
                params: { category: category }
            });
            tickets = response.data;
        } catch (error) {
            console.error('Error fetching tickets:', error);
        }
    }

    // Fetch tickets on component mount
    onMount(() => fetchTickets());

    // Handle category change with if-else condition
    function handleCategoryChange(event) {
        selectedCategory = event.target.value;
        fetchTickets(selectedCategory);
    }
</script>
<body>
<h1>Ticket Listing</h1>

<label for="category">Filter by Category:</label>
<select id="category" on:change={handleCategoryChange}>
    <option value="" >All</option>
    {#each categories as category}
        <option value={category}>{category}</option>
    {/each}
</select>

<table>
    <thead>
        <tr>
            <th>Category</th>
            <th>Title</th>
            <th>Description</th>
            <th>Status</th>
            <th>Priority</th>
        </tr>
    </thead>
    <tbody>
        {#each tickets as ticket}
            <tr>
                <td>{ticket.category}</td>
                <td>{ticket.title}</td>
                <td>{ticket.description}</td>
                <td>{ticket.status}</td>
                <td>{ticket.priority}</td>
            </tr>
        {/each}
    </tbody>
</table>
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
    }

    option{
        width: 55px;
        margin-left:0px;
    }

    label {
        margin-bottom: 10px;
        margin-left: 400px;
        font-size: 16px;
        color:#E5EAF5;
    }
    select {
        margin-left:10px;
        padding:0px;
        background-color:#E8175D;
        color:#E5EAF5;
    }
    

    table {
        width: 200%;
        max-width: 700px;
        max-height: 800px;
        border-collapse: collapse;
        margin-top: 20px;
        margin-left: 400px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        overflow: hidden;
        background:#A8A7A7;
    
    }

    th, td {
        padding: 10px;
        border: 1px solid #363636;
        text-align: left;
    }

    th {
        background:#E8175D;
        color: white;
    }

    tr:nth-child(even) {
        background:#A8A7A7;
    }
</style>
