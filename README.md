<!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Курсы валют и конвертер</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                background-color: #f4f4f9;
                color: #333;
                margin: 0;
                padding: 0;
            }
            h1, h2 {
                text-align: center;
                background-color: #333;
                color: white;
                padding: 1em 0;
                margin: 0;
            }
            .container {
                max-width: 600px;
                margin: 20px auto;
                padding: 20px;
                background: white;
                border-radius: 8px;
                box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            }
            table {
                width: 100%;
                border-collapse: collapse;
                margin-bottom: 20px;
            }
            table, th, td {
                border: 1px solid #ddd;
            }
            th, td {
                padding: 10px;
                text-align: center;
            }
            form {
                display: flex;
                flex-direction: column;
                gap: 10px;
            }
            input, select, button {
                padding: 10px;
                font-size: 16px;
                border: 1px solid #ddd;
                border-radius: 4px;
            }
            button {
                background-color: #333;
                color: white;
                border: none;
                cursor: pointer;
            }
            button:hover {
                background-color: #555;
            }
        </style>
    </head>
    <body>
        <h1>Курсы валют</h1>
        <div class="container">
            <table>
                <thead>
                    <tr>
                        <th>Валюта</th>
                        <th>Покупка</th>
                        <th>Продажа</th>
                    </tr>
                </thead>
                <tbody id="rates-table">
                </tbody>
            </table>
            <h2>Конвертер валют</h2>
            <form onsubmit="convertCurrency(event)">
                <label for="from_currency">Из валюты:</label>
                <select name="from_currency" id="from_currency" required></select>
                <label for="to_currency">В валюту:</label>
                <select name="to_currency" id="to_currency" required></select>
                <label for="amount">Сумма:</label>
                <input type="number" step="0.01" name="amount" id="amount" required>
                <button type="submit">Конвертировать</button>
            </form>
            <h3 id="result"></h3>
        </div>
        <script>
            const rates = {"USD": {"buy": 529.5, "sell": 516.3}, "EUR": {"buy": 554.5, "sell": 540.5}, "RUB": {"buy": 5.07, "sell": 4.89}, "KGS": {"buy": 5.99, "sell": 5.55}, "GBP": {"buy": 671.0, "sell": 641.0}, "CNY": {"buy": 75.5, "sell": 71.5}};

            // Заполняем таблицу курсов
            const ratesTable = document.getElementById('rates-table');
            for (const [currency, rate] of Object.entries(rates)) {
                const row = `<tr>
                    <td>${currency}</td>
                    <td>${rate.buy}</td>
                    <td>${rate.sell}</td>
                </tr>`;
                ratesTable.innerHTML += row;
            }

            // Заполняем выпадающие списки
            const fromCurrency = document.getElementById('from_currency');
            const toCurrency = document.getElementById('to_currency');
            for (const currency of Object.keys(rates)) {
                const option = `<option value="${currency}">${currency}</option>`;
                fromCurrency.innerHTML += option;
                toCurrency.innerHTML += option;
            }

            // Конвертация валют
            function convertCurrency(event) {
                event.preventDefault();
                const from = fromCurrency.value;
                const to = toCurrency.value;
                const amount = parseFloat(document.getElementById('amount').value);

                if (rates[from] && rates[to]) {
                    const result = (amount * rates[from].sell / rates[to].buy).toFixed(2);
                    document.getElementById('result').textContent = `Результат: ${result} ${to}`;
                } else {
                    document.getElementById('result').textContent = 'Ошибка при конверсии.';
                }
            }
        </script>
    </body>
    </html>
    
