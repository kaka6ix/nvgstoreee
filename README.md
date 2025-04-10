<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>nvgstore</title>
  <style>
    body {
      font-family: sans-serif;
      margin: 0;
      padding: 0;
      background-color: #fff;
      color: #000;
    }
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1rem 2rem;
      border-bottom: 1px solid #ddd;
    }
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1rem;
      padding: 2rem;
    }
    .card {
      border: 1px solid #eee;
      padding: 1rem;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.05);
    }
    button {
      margin-top: 0.5rem;
      padding: 0.5rem 1rem;
      border: none;
      background: #000;
      color: #fff;
      cursor: pointer;
      border-radius: 4px;
    }
    #cart-info {
      font-weight: bold;
    }
  </style>
</head>
<body>

<header>
  <h1>daniwisnu</h1>
  <div id="cart-info">0 item(s) - Rp 0</div>
</header>

<div class="product-grid" id="product-list"></div>

<script>
  const products = [
    { id: 1, name: "Kaos Hitam Polos", price: 120000 },
    { id: 2, name: "Kemeja Flanel", price: 180000 },
    { id: 3, name: "Hoodie Oversize", price: 250000 },
  ];

  const cart = [];

  const cartInfo = document.getElementById("cart-info");
  const productList = document.getElementById("product-list");

  function updateCart() {
    const total = cart.reduce((sum, item) => sum + item.price, 0);
    cartInfo.textContent = `${cart.length} item(s) - Rp ${total.toLocaleString()}`;
  }

  function addToCart(product) {
    cart.push(product);
    updateCart();
  }

  products.forEach(product => {
    const card = document.createElement("div");
    card.className = "card";
    card.innerHTML = `
      <h2>${product.name}</h2>
      <p>Rp ${product.price.toLocaleString()}</p>
      <button onclick='addToCart(${JSON.stringify(product)})'>Tambah ke Keranjang</button>
    `;
    productList.appendChild(card);
  });

  // trick to allow passing object via onclick
  window.addToCart = addToCart;
</script>

</body>
</html>
