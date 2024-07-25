<script>
    import { onMount } from 'svelte';
    import axios from 'axios';
    import { navigate } from 'svelte-routing';
    import Page from '../ticketsraising/+page.svelte';

    let tickets = [];
    let filteredCategory = ''; // State to store selected category filter
  
    const fetchTickets = async () => {
      try {
        const response = await axios.get('http://localhost:3000/tickets');
        tickets = response.data;
      } catch (error) {
        console.error('Error fetching tickets:', error);
      }
    };
  
    onMount(fetchTickets);
  
    // Function to filter tickets by category
    const filterTickets = (category) => {
      if (category === '') {
        fetchTickets(); // Reset to fetch all tickets if category is empty
      } else {
        tickets = tickets.filter(ticket => ticket.category === category);
      }
    };
  
    // Function to navigate to the Add Ticket page
    const navigateToAddTicket = () => {
      navigate('http://localhost:5173/ticketsraising'); // Adjust the route as per your application setup
    };
  </script>
<!-- creating a nav bar-->
<ul>
  <li class="ticketsystem"> TICKET SUPPORT SYSTEM </li>
  <li> <button class="logout", type="button">logout</button> </li>
  <li class="username"> username </li>
</ul>

  <h1>Ticket Listing</h1>
  
  <div class="filter-container">
    <label>
      Filter by Category:
      <select bind:value={filteredCategory} on:change={() => filterTickets(filteredCategory)}>
        <option value="">All Categories</option>
        <option value="Bug">Bug</option>
        <option value="Feature Request">Feature Request</option>
        <option value="Support">Support</option>
        <option value="Payment">Payment</option>
        <option value="Others">Others</option>
      </select>
    </label>
    <a href="http://localhost:5173/ticketsraising"><button class="add-ticket-btn" on:click={navigateToAddTicket}>Add Ticket</button></a>
  </div>
  
  <table>
    <thead>
      <tr>
        <th>ID</th>
        <th>Category</th>
        <th>Title</th>
        <th>Description</th>
        <th>Priority</th>
      </tr>
    </thead>
    <tbody>
      {#each tickets as ticket}
        <tr>
          <td>{ticket.id}</td>
          <td>{ticket.category}</td>
          <td>{ticket.title}</td>
          <td>{ticket.description}</td>
          <td>{ticket.priority}</td>
        </tr>
      {/each}
      {#if tickets.length === 0}
        <tr>
          <td colspan="5" style="text-align: center;">No tickets found.</td>
        </tr>
      {/if}
    </tbody>
  </table>
  
  
  <style>
    h1 {
      text-align: center;
      margin-bottom: 20px;
    }
  
    label{
    margin-left: 390px;
    }

    table {
        width: 100%;
        max-width: 700px;
        border-collapse: collapse;
        margin-top: 20px;
        margin-left: auto;
        margin-right: auto;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        background: #A8A7A7;
    }

    th, td { 
        padding: 10px;
        border: 1px solid #363636;
        text-align: left;
    }
  
    th {
        background: #E8175D;
        color: white;
    }
  
    tbody tr:nth-child(even) {
      background-color: #ffffff;
    }
  
    tbody tr:hover {
      background-color: #e0e0e0;
      cursor: pointer;
    }
  
    .filter-container select {
      padding: 8px;
      border-radius: 4px;
      border: 1px solid #ccc;
      font-size: 14px;
      transition: border-color 0.3s ease, transform 0.3s ease;
      margin-left:auto;
    }
  
    .add-ticket-btn {
      background-color: #E8175D;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      margin-left:325px ;
    }
  
    .add-ticket-btn:hover {
      background-color: #c2144e;
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
        margin-top:10px;
        
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
        line-height:50px;
        margin-left:20px;
    }
    .username{
        float:right;
        line-height:50px;
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        font-size: 20px;
    }
  </style>