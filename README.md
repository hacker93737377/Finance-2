 html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Finanz Tracker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 300px;
        }
        h1, h2 {
            text-align: center;
        }
        form {
            display: flex;
            flex-direction: column;
        }
        input, select, button {
            margin: 5px 0;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            background-color: #28a745;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background: #f8f9fa;
            margin: 5px 0;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            display: flex;
            justify-content: space-between;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Finanz Tracker</h1>
        <form id="transaction-form">
            <input type="text" id="description" placeholder="Beschreibung" required>
            <input type="number" id="amount" placeholder="Betrag" required>
            <select id="type">
                <option value="income">Einnahme</option>
                <option value="expense">Ausgabe</option>
            </select>
            <button type="submit">Hinzufügen</button>
        </form>
        <h2>Transaktionen</h2>
        <ul id="transaction-list"></ul>
        <h2>Saldo: <span id="balance">0</span>€</h2>
    </div>
    <script>
        document.getElementById('transaction-form').addEventListener('submit', function(event) {
            event.preventDefault();
            const description = document.getElementById('description').value;
            const amount = parseFloat(document.getElementById('amount').value);
            const type = document.getElementById('type').value;
            if (description && amount) {
                addTransaction(description, amount, type);
                updateBalance();
                document.getElementById('transaction-form').reset();
            }
        });
        function addTransaction(description, amount, type) {
            const transactionList = document.getElementById('transaction-list');
            const li = document.createElement('li');
            li.innerHTML = `
                <span>${description}</span>
                <span>${type === 'income' ? '+' : '-'}${amount.toFixed(2)}€</span>
            `;
            transactionList.appendChild(li);
        }
        function updateBalance() {
            const transactions = document.querySelectorAll('#transaction-list li');
            let balance = 0;
            transactions.forEach(transaction => {
                const amountText = transaction.querySelector('span:last-child').textContent;
                const amount = parseFloat(amountText.replace('€', ''));
                balance += amount;
            });
            document.getElementById('balance').textContent = balance.toFixed(2);
        }
    </script>
</body>
</html>
