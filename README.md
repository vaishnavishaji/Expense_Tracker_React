# Expense Tracker (ReactJS)
## Date:24-05-2025

## AIM
To develop a simple Expense Tracker application using React that allows users to manage their personal finances by adding, viewing, and deleting income and expense transactions, while dynamically calculating the current balance, total income, and total expenses.

## ALGORITHM
### STEP 1: Initialize the Project
Create a new React app using:

npx create-react-app expense-tracker
or

npm create vite@latest expense-tracker --template react

Open the project in a code editor like VS Code.

### Step 2: Setup State
Define a state variable to store transactions:

Example: const [transactions, setTransactions] = useState([])

Define state variables for the form inputs:

const [text, setText] = useState("")

const [amount, setAmount] = useState("")

### Step 3: Add a New Transaction
Create a form with two inputs:

Text input for description

Number input for amount

On form submit:

Validate input

Create a new transaction object

Add the object to the transactions array using setTransactions.

### Step 4: Display Transaction List

Use map() to render each transaction in a list.

Conditionally style each item based on amount > 0 (income) or amount < 0 (expense).

Add a delete button next to each transaction.

### Step 5: Calculate and Display Summary

Use reduce() to calculate:

Total Balance: sum of all amounts

Total Income: sum of all positive amounts

Total Expenses: sum of all negative amounts

Display these values at the top of the UI.

### Step 6: Delete a Transaction

When delete is clicked:

Use filter() to remove the transaction from the array by id.

Update the state using setTransactions.

### Step 7: Style the Application

Use basic CSS to style:

Balance summary

Income/expense totals

Form inputs

Transaction list (with color coding)

## PROGRAM
```
import React, { useState } from 'react';

export default function ExpenseTracker() {
  const [transactions, setTransactions] = useState([]);
  const [description, setDescription] = useState('');
  const [amount, setAmount] = useState('');

  const handleAddTransaction = (e) => {
    e.preventDefault();
    if (!description || isNaN(amount) || amount === 0) return;

    const newTransaction = {
      id: Date.now(),
      description,
      amount: parseFloat(amount)
    };

    setTransactions([newTransaction, ...transactions]);
    setDescription('');
    setAmount('');
  };

  const handleDelete = (id) => {
    setTransactions(transactions.filter(tx => tx.id !== id));
  };

  const total = transactions.reduce((acc, tx) => acc + tx.amount, 0).toFixed(2);
  const income = transactions
    .filter(tx => tx.amount > 0)
    .reduce((acc, tx) => acc + tx.amount, 0).toFixed(2);
  const expense = transactions
    .filter(tx => tx.amount < 0)
    .reduce((acc, tx) => acc + tx.amount, 0).toFixed(2);

  return (
    <div className="max-w-md mx-auto p-4 bg-white shadow-lg rounded-xl mt-8">
      <h2 className="text-2xl font-bold mb-4 text-center">Expense Tracker</h2>

      <div className="text-center mb-6">
        <h3 className="text-xl font-semibold">Balance: ${total}</h3>
      </div>

      <div className="flex justify-between mb-6">
        <div className="bg-green-100 text-green-700 p-4 rounded w-1/2 mr-2 text-center">
          <h4>Income</h4>
          <p>+${income}</p>
        </div>
        <div className="bg-red-100 text-red-700 p-4 rounded w-1/2 ml-2 text-center">
          <h4>Expense</h4>
          <p>${Math.abs(expense)}</p>
        </div>
      </div>

      <form onSubmit={handleAddTransaction} className="mb-6">
        <input
          type="text"
          value={description}
          onChange={(e) => setDescription(e.target.value)}
          placeholder="Description"
          className="w-full mb-2 p-2 border rounded"
        />
        <input
          type="number"
          value={amount}
          onChange={(e) => setAmount(e.target.value)}
          placeholder="Amount (+ for income, - for expense)"
          className="w-full mb-2 p-2 border rounded"
        />
        <button className="w-full bg-blue-500 text-white p-2 rounded">Add Transaction</button>
      </form>

      <h4 className="text-lg font-semibold mb-2">Transactions</h4>
      <ul>
        {transactions.map(tx => (
          <li
            key={tx.id}
            className={`flex justify-between items-center p-2 mb-2 border-l-4 ${tx.amount >= 0 ? 'border-green-500' : 'border-red-500'} bg-gray-100 rounded`}
          >
            <span>{tx.description}</span>
            <div className="flex items-center space-x-2">
              <span className="font-mono">{tx.amount >= 0 ? '+' : ''}${tx.amount.toFixed(2)}</span>
              <button
                onClick={() => handleDelete(tx.id)}
                className="text-red-600 hover:text-red-800"
              >
                &#10006;
              </button>
            </div>
          </li>
        ))}
      </ul>
    </div>
  );
}
```


## OUTPUT
![Screenshot 2025-05-24 133838](https://github.com/user-attachments/assets/49e17ef3-6bae-4d91-934e-8ee25e465c09)


## RESULT
A fully functional React-based Expense Tracker application was successfully developed. 
