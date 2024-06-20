<script>
    import { onMount } from 'svelte';
    import axios from 'axios';

    let tickets = [];

    // Function to fetch all tickets
    async function fetchTickets() {
        try {
            const response = await axios.get('http://localhost:3000/tickets');
            tickets = response.data;
        } catch (error) {
            console.error('Error fetching tickets:', error);
        }
    }

    // Fetch tickets on component mount
    onMount(fetchTickets);
</script>
<body>
<h1>Ticket List</h1>
<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Title</th>
            <th>Description</th>
            <th>Status</th>
        </tr>
    </thead>
    <tbody>
        {#each tickets as ticket}
        <tr>
            <td>{ticket.id}</td>
            <td>{ticket.title}</td>
            <td>{ticket.description}</td>
            <td>{ticket.status}</td>
        </tr>
        {:else}
        <tr>
            <td colspan="4">No tickets found</td>
        </tr>
        {/each}
    </tbody>
</table>

<style>
    body{
        background-color:#3AAFA9;
    }
    tbody {
        font-family: Arial, sans-serif;
        background-color: #f0f2f5;
        margin:0 ;
        padding: 0;
        display: flexbox;
        flex-direction: column;
        align-items: center;
        
    }

    h1 {
        color:#17252A;
        text-align: center;
        margin-top: 20px;
    }

    table {
        width: 100%;
        max-width: 500px;
        margin: 0 auto;
        border-collapse: collapse;
        margin-top: 20px;
        background: white;
        box-shadow: 0 2px 4px rgba(3, 28, 69, 0.1);
        border-radius: 8px;
        overflow: hidden;
    }

    th, td {
        padding: 15px;
        text-align: left;
        border-bottom: 1px solid #ddd;
    }

    th {
        background-color: #2B7A78;
        color: white;
        font-weight: bold;
    }

    tbody tr:nth-child(even) {
        background-color: #f2f2f2;
    }

    tbody tr:hover {
        background-color: #ddd;
    }

    td {
        color:#17252A;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        max-width: 300px;
        
    }

    td:first-child {
        width: 50px;
    }
</style>
</body>