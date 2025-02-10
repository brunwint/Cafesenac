<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CaféSenac - Lanches Online</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #ff7f00, #ff6600);
            color: #333;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }
        header {
            background-color: #333;
            color: white;
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        header .logo {
            display: flex;
            align-items: center;
        }
        header .logo h1 {
            font-size: 24px;
            margin-right: 10px;
        }
        header .cart button {
            background-color: #ff6600;
            color: white;
            border: none;
            padding: 10px 15px;
            cursor: pointer;
            margin-left: 10px;
        }
        .menu {
            padding: 20px;
            text-align: center;
        }
        .menu h2 {
            margin-bottom: 20px;
            font-size: 28px;
            color: white;
        }
        .products {
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
        }
        .product {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 15px;
            text-align: center;
            width: 200px;
            margin: 10px;
        }
        .product img {
            width: 100%;
            border-radius: 10px;
        }
        .product .price {
            font-size: 18px;
            font-weight: bold;
            margin: 10px 0;
        }
        .product button {
            background-color: #28a745;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
            border-radius: 5px;
        }
        .cart-popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            width: 300px;
            z-index: 100;
        }
        .cart-popup ul {
            list-style: none;
            margin-bottom: 20px;
        }
        .cart-popup ul li {
            margin: 10px 0;
        }
        footer {
            text-align: center;
            padding: 10px;
            background-color: #333;
            color: white;
            margin-top: auto;
        }
        .payment-form {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .payment-form p {
            margin-bottom: 15px;
            font-size: 14px;
            color: #555;
            text-align: center;
        }
        .payment-form input[type="checkbox"] {
            margin-right: 10px;
        }
        .payment-form label {
            font-size: 14px;
            color: #555;
        }
        .payment-form input[type="text"],
        .payment-form input[type="email"],
        .payment-form input[type="tel"],
        .payment-form select {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        .payment-form button {
            padding: 10px;
            background-color: #ff6600;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            width: 100%;
        }
        .payment-form button:hover {
            background-color: #ff7f00;
        }
        #pix-qr-code {
            display: none;
            text-align: center;
            margin-top: 20px;
        }
        #pix-qr-code img {
            width: 300px;
            height: auto;
        }
        header .logo img {
            height: 40px;
            width: auto;
        }
        .order-note {
            padding: 20px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            text-align: left;
            font-family: Arial, sans-serif;
            color: #333;
            width: 400px;
            margin: 20px auto;
        }
        .order-note h3 {
            text-align: center;
            font-size: 24px;
            margin-bottom: 10px;
        }
        .order-note p {
            margin: 5px 0;
        }
        .download-btn {
            display: block;
            width: 200px;
            margin: 20px auto;
            padding: 10px;
            text-align: center;
            background-color: #28a745;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .download-btn:hover {
            background-color: #218838;
        }
        .back-to-start-btn {
            display: block;
            width: 200px;
            margin: 20px auto;
            padding: 10px;
            text-align: center;
            background-color: #ff6600;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .back-to-start-btn:hover {
            background-color: #ff7f00;
        }
        .orders-popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            width: 400px;
            z-index: 100;
            max-height: 80vh;
            overflow-y: auto;
        }
        .orders-popup h2 {
            text-align: center;
            margin-bottom: 20px;
        }
        .orders-popup ul {
            list-style: none;
            padding: 0;
        }
        .orders-popup ul li {
            margin-bottom: 15px;
            padding: 10px;
            background-color: #f9f9f9;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .cancel-btn {
            background-color: #ff0000;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
        }
        .cancel-btn:hover {
            background-color: #cc0000;
        }
    </style>
</head>
<body>
    <header>
        <div class="logo">
            <h1>CaféSenac</h1>
            <img src="https://www.ba.senac.br/assets/template/images/senac_logo_branco.png" alt="Logo Senac">
        </div>
        <div class="cart">
            <button onclick="showCart()">Carrinho (0)</button>
            <button onclick="showOrders()">Notas de Pedidos</button>
        </div>
    </header>
    <main id="menu-section">
        <section class="menu">
            <h2>Nosso Cardápio</h2>
            <div class="products">
                <div class="product" id="hamburguer">
                    <img src="https://assets.unileversolutions.com/recipes-v2/230411.jpg" alt="Hamburguer Clássico">
                    <h3>Hambúrguer Premium</h3>
                    <p>Hambúrguer premium recheado com lombo canadense, queijo cheddar, bacon empanado, alface, tomate e molho premium.</p>
                    <p class="price">R$ 8,00</p>
                    <button onclick="addToCart('Hambúrguer Premium', 8)">Adicionar ao Carrinho</button>
                </div>
                <div class="product" id="coxinha">
                    <img src="https://swiftbr.vteximg.com.br/arquivos/ids/203103-636-636/617666-coxinha-de-frango-mandioca-pre-frita_1.jpg?v=638682505691470000" alt="Coxinha de Frango">
                    <h3>Coxinha de Frango</h3>
                    <p>Coxinha crocante quente com recheio de frango com catupiry, presunto e queijo e carne.</p>
                    <p class="price">R$ 2,00</p>
                    <button onclick="addToCart('Coxinha de Frango', 2)">Adicionar ao Carrinho</button>
                </div>
                <div class="product" id="refri">
                    <img src="https://theburger.vendanaweb.com.br/_core/_uploads/55/2021/07/2218290721ed89khiec5.jpeg" alt="Refrigerante">
                    <h3>Refrigerante Lata</h3>
                    <p>Bebidas como Coca-Cola, Fanta, Sprite e H2O.</p>
                    <p class="price">R$ 5,00</p>
                    <button onclick="addToCart('Refrigerante Lata', 5)">Adicionar ao Carrinho</button>
                </div>
                <div class="product" id="bolos">
                    <img src="https://docequintalconfeitaria.com/wp-content/uploads/2023/06/brownie-vender-scaled.jpg" alt="Bolos Recheados">
                    <h3>Bolos Recheados</h3>
                    <p>Bolos especiais recheados, Sabor Morango, Chocolate, Cenoura e Red Velvet.</p>
                    <p class="price">R$ 8,00 por fatia</p>
                    <button onclick="addToCart('Bolo Recheado', 8)">Adicionar ao Carrinho</button>
                </div>
            </div>
        </section>
    </main>
    <section class="cart-popup" id="cart-popup">
        <h2>Seu Carrinho</h2>
        <ul id="cart-items"></ul>
        <p>Total: R$ <span id="total-price">0</span></p>
        <button onclick="checkout()">Finalizar Compra</button>
        <button onclick="goBackToMenu()">Voltar ao Menu</button>
    </section>
    <section class="payment-form" id="payment-form">
        <h2>Formulário de Pagamento</h2>
        <p>
            Atenção: seus dados serão incluídos com o objetivo de recomendar nossas atualizações, 
            informá-lo sobre nosso negócio e nossa campanha de marketing.
        </p>
        <div>
            <input type="checkbox" id="agree-terms" name="agree-terms" required>
            <label for="agree-terms">Concordo com as diretrizes presentes.</label>
        </div>
        <form id="payment-form-content" onsubmit="handlePayment(event)">
            <label for="name">Nome:</label>
            <input type="text" id="name" name="name" required>
            <label for="email">E-mail:</label>
            <input type="email" id="email" name="email" required>
            <label for="phone">Telefone:</label>
            <input type="tel" id="phone" name="phone" required>
            <label for="interval-time">Horário de Intervalo:</label>
            <select id="interval-time" name="interval-time" required>
                <option value="">Selecione um horário</option>
                <option value="08:00">08:00</option>
                <option value="08:30">08:30</option>
                <option value="09:00">09:00</option>
                <option value="09:30">09:30</option>
                <option value="10:00">10:00</option>
                <option value="10:30">10:30</option>
                <option value="11:00">11:00</option>
                <option value="11:30">11:30</option>
                <option value="12:00">12:00</option>
                <option value="12:30">12:30</option>
                <option value="13:00">13:00</option>
                <option value="13:30">13:30</option>
                <option value="14:00">14:00</option>
                <option value="14:30">14:30</option>
                <option value="15:00">15:00</option>
                <option value="15:30">15:30</option>
                <option value="16:00">16:00</option>
                <option value="16:30">16:30</option>
                <option value="17:00">17:00</option>
                <option value="17:30">17:30</option>
                <option value="18:00">18:00</option>
                <option value="18:30">18:30</option>
                <option value="19:00">19:00</option>
                <option value="19:30">19:30</option>
                <option value="20:00">20:00</option>
                <option value="20:30">20:30</option>
                <option value="21:00">21:00</option>
                <option value="21:30">21:30</option>
            </select>
            <label for="payment-method">Método de Pagamento:</label>
            <select id="payment-method" name="payment-method" onchange="togglePixQRCode()" required>
                <option value="credit-card">Cartão</option>
                <option value="pix">PIX</option>
                <option value="money">Dinheiro</option>
            </select>
            <button type="submit">Finalizar Pedido</button>
        </form>
        <div id="pix-qr-code">
            <img src="https://media.istockphoto.com/id/1347277582/vector/qr-code-sample-for-smartphone-scanning-on-white-background.jpg?s=612x612&w=0&k=20&c=6e6Xqb1Wne79bJsWpyyNuWfkrUgNhXR4_UYj3i_poc0=" alt="QR Code PIX">
            <p>Digite ou QR Code para concluir o pagamento via PIX.</p>
        </div>
    </section>
    <section class="orders-popup" id="orders-popup">
        <h2>Notas de Pedidos</h2>
        <ul id="orders-list"></ul>
        <button onclick="closeOrders()">Fechar</button>
    </section>
    <footer>
        <p>© 2024 CaféSenac - Todos os direitos reservados.</p>
    </footer>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/0.4.1/html2canvas.min.js"></script>
    <script>
        let cart = [];
        let total = 0;
        let orders = [];

        function addToCart(item, price) {
            cart.push({ item, price });
            total += price;
            document.querySelector('.cart button').innerText = `Carrinho (${cart.length})`;
            alert("ATENÇÃO! Seu produto foi adicionado ao carrinho!");
        }

        function removeFromCart(index) {
            total -= cart[index].price;
            cart.splice(index, 1);
            document.querySelector('.cart button').innerText = `Carrinho (${cart.length})`;
            showCart();
        }

        function showCart() {
            let cartItems = document.getElementById('cart-items');
            cartItems.innerHTML = '';
            cart.forEach((item, index) => {
                let li = document.createElement('li');
                li.innerHTML = `${item.item} - R$ ${item.price.toFixed(2)} <button onclick="removeFromCart(${index})">Excluir</button>`;
                cartItems.appendChild(li);
            });
            document.getElementById('total-price').innerText = total.toFixed(2);
            document.getElementById('cart-popup').style.display = 'block';
            document.getElementById('menu-section').style.display = 'none';
        }

        function goBackToMenu() {
            document.getElementById('cart-popup').style.display = 'none';
            document.getElementById('menu-section').style.display = 'block';
        }

        function checkout() {
            document.getElementById('cart-popup').style.display = 'none';
            document.getElementById('payment-form').style.display = 'flex';
        }

        function togglePixQRCode() {
            const paymentMethod = document.getElementById('payment-method').value;
            const pixQRCode = document.getElementById('pix-qr-code');
            if (paymentMethod === 'pix') {
                pixQRCode.style.display = 'block';
            } else {
                pixQRCode.style.display = 'none';
            }
        }

        function handlePayment(event) {
            event.preventDefault();
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const phone = document.getElementById('phone').value;
            const intervalTime = document.getElementById('interval-time').value;
            const paymentMethod = document.getElementById('payment-method').value;
            const randomNumbers = Math.floor(1000 + Math.random() * 9000);
            let orderDetails = {
                number: randomNumbers,
                name,
                email,
                phone,
                intervalTime,
                paymentMethod,
                items: cart.map(item => `${item.item} - R$ ${item.price.toFixed(2)}`),
                total: total.toFixed(2)
            };
            orders.push(orderDetails);
            localStorage.setItem('orders', JSON.stringify(orders));
            let orderNote = `<div class="order-note" id="order-note">
                                <h3>Nota de Pedido</h3>
                                <p><strong>Número do Pedido:</strong> ${randomNumbers}</p>
                                <p><strong>Nome:</strong> ${name}</p>
                                <p><strong>E-mail:</strong> ${email}</p>
                                <p><strong>Telefone:</strong> ${phone}</p>
                                <p><strong>Horário de Intervalo:</strong> ${intervalTime}</p>
                                <p><strong>Método de Pagamento:</strong> ${paymentMethod}</p>
                                <p><strong>Itens do Pedido:</strong></p>`;
            cart.forEach(item => {
                orderNote += `<p>${item.item} - R$ ${item.price.toFixed(2)}</p>`;
            });
            orderNote += `<p><strong>Total do Pedido:</strong> R$ ${total.toFixed(2)}</p>`;
            orderNote += `<p><strong>Aviso:</strong> Seu pedido estará em "Notas de Pedidos" no cabeçalho.</p></div>`;
            orderNote += `<button class="back-to-start-btn" onclick="backToStart()">Voltar para o Início</button>`;
            document.body.innerHTML += orderNote;
            html2canvas(document.getElementById('order-note')).then(function(canvas) {
                var imgData = canvas.toDataURL('image/png');
                var downloadLink = document.createElement('a');
                downloadLink.href = imgData;
                downloadLink.download = 'nota-de-pedido.png';
                downloadLink.classList.add('download-btn');
                downloadLink.innerText = 'Baixar Nota de Pedido';
                document.body.appendChild(downloadLink);
            });
        }

        function backToStart() {
            cart = [];
            total = 0;
            document.querySelector('.cart button').innerText = 'Carrinho (0)';
            const orderNote = document.querySelector('.order-note');
            const backToStartBtn = document.querySelector('.back-to-start-btn');
            const downloadBtn = document.querySelector('.download-btn');
            if (orderNote) orderNote.remove();
            if (backToStartBtn) backToStartBtn.remove();
            if (downloadBtn) downloadBtn.remove();
            document.getElementById('menu-section').style.display = 'block';
            document.getElementById('cart-popup').style.display = 'none';
            document.getElementById('payment-form').style.display = 'none';
        }

        function showOrders() {
            const ordersList = document.getElementById('orders-list');
            ordersList.innerHTML = '';
            const storedOrders = JSON.parse(localStorage.getItem('orders')) || [];
            if (storedOrders.length === 0) {
                ordersList.innerHTML = '<p>Nenhum pedido encontrado.</p>';
            } else {
                storedOrders.forEach((order, index) => {
                    let li = document.createElement('li');
                    li.innerHTML = `
                        <p><strong>Número do Pedido:</strong> ${order.number}</p>
                        <p><strong>Nome:</strong> ${order.name}</p>
                        <p><strong>E-mail:</strong> ${order.email}</p>
                        <p><strong>Telefone:</strong> ${order.phone}</p>
                        <p><strong>Horário de Intervalo:</strong> ${order.intervalTime}</p>
                        <p><strong>Método de Pagamento:</strong> ${order.paymentMethod}</p>
                        <p><strong>Itens do Pedido:</strong></p>
                        <ul>${order.items.map(item => `<li>${item}</li>`).join('')}</ul>
                        <p><strong>Total do Pedido:</strong> R$ ${order.total}</p>
                        <button class="cancel-btn" onclick="cancelOrder(${index})">Cancelar pedido</button>
                    `;
                    ordersList.appendChild(li);
                });
            }
            document.getElementById('orders-popup').style.display = 'block';
        }

        function cancelOrder(index) {
            let storedOrders = JSON.parse(localStorage.getItem('orders')) || [];
            storedOrders.splice(index, 1);
            localStorage.setItem('orders', JSON.stringify(storedOrders));
            alert('ATENÇÃO! SEU PEDIDO FOI CANCELADO.');
            showOrders();
        }

        function closeOrders() {
            document.getElementById('orders-popup').style.display = 'none';
        }

        window.onload = function() {
            const storedOrders = JSON.parse(localStorage.getItem('orders')) || [];
            orders = storedOrders;
        };
    </script>
</body>
</html>
