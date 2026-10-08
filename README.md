<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Good Food — Order Online</title>
  <style>
    * { box-sizing: border-box; }
    body { margin: 0; font-family: Arial, sans-serif; color: #27251f; background: #fffaf2; }
    header { padding: 18px 7%; display: flex; justify-content: space-between; align-items: center; background: white; }
    .logo { font-size: 1.4rem; font-weight: 800; color: #e4572e; }
    .cart-button, .add-button { border: 0; border-radius: 9px; padding: 11px 16px; background: #e4572e; color: white; font-weight: bold; cursor: pointer; }
    .hero { padding: 70px 7%; background: #ffe8cc; }
    .hero h1 { max-width: 600px; margin: 0 0 12px; font-size: clamp(2.4rem, 6vw, 4.5rem); }
    .hero p { font-size: 1.1rem; color: #5d554a; }
    main { padding: 36px 7%; }
    .menu { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
    .item { background: white; border-radius: 14px; overflow: hidden; box-shadow: 0 5px 18px #39230d12; }
    .item img { display: block; width: 100%; height: 170px; object-fit: cover; }
    .item-content { padding: 16px; }
    .item h2 { margin: 0 0 8px; font-size: 1.2rem; }
    .item p { color: #70695f; min-height: 38px; }
    .item-bottom { display: flex; justify-content: space-between; align-items: center; }
    footer { padding: 24px 7%; text-align: center; color: #70695f; }
    dialog { border: 0; border-radius: 14px; width: min(420px, 92vw); padding: 24px; box-shadow: 0 10px 40px #0004; }
    dialog::backdrop { background: #0007; }
    .cart-row { display: flex; justify-content: space-between; gap: 12px; margin: 12px 0; }
  </style>
</head>
<body>
  <header>
    <div class="logo">🍊 Good Food</div>
    <button class="cart-button" onclick="showCart()">Cart (<span id="cart-count">0</span>)</button>
  </header>

  <section class="hero">
    <h1>Fresh food, delivered with love.</h1>
    <p>Good ingredients. Big flavors. Right at your door.</p>
  </section>

  <main>
    <h2>Popular dishes</h2>
    <div class="menu" id="menu"></div>
  </main>

  <footer>Made fresh daily · Open 11am–10pm</footer>

  <dialog id="cart-dialog">
    <h2>Your order</h2>
    <div id="cart-items"></div>
    <p><strong>Total: $<span id="total">0.00</span></strong></p>
    <button class="add-button" onclick="checkout()">Checkout</button>
    <button onclick="document.querySelector('dialog').close()">Close</button>
  </dialog>

  <script>
    const dishes = [
      { name: "Classic Burger", description: "Grilled beef, cheddar, and house sauce.", price: 9.50, image: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?auto=format&fit=crop&w=800&q=80" },
      { name: "Garden Salad", description: "Fresh greens, tomatoes, and lemon dressing.", price: 7.00, image: "https://images.unsplash.com/photo-1512621776951-a57141f2eefd?auto=format&fit=crop&w=800&q=80" },
      { name: "Margherita Pizza", description: "Tomato, mozzarella, and fresh basil.", price: 12.00, image: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002?auto=format&fit=crop&w=800&q=80" },
      { name: "Berry Pancakes", description: "Fluffy pancakes with berries and maple syrup.", price: 8.00, image: "https://images.unsplash.com/photo-1528207776546-365bb710ee93?auto=format&fit=crop&w=800&q=80" }
    ];

    const cart = [];

    document.getElementById("menu").innerHTML = dishes.map((dish, index) => `
      <article class="item">
        <img src="${dish.image}" alt="${dish.name}">
        <div class="item-content">
          <h2>${dish.name}</h2>
          <p>${dish.description}</p>
          <div class="item-bottom">
            <strong>$${dish.price.toFixed(2)}</strong>
            <button class="add-button" onclick="addToCart(${index})">Add</button>
          </div>
        </div>
      </article>
    `).join("");

    function addToCart(index) {
      cart.push(dishes[index]);
      document.getElementById("cart-count").textContent = cart.length;
    }

    function showCart() {
      const rows = cart.map(dish => `<div class="cart-row"><span>${dish.name}</span><span>$${dish.price.toFixed(2)}</span></div>`).join("") || "<p>Your cart is empty.</p>";
      document.getElementById("cart-items").innerHTML = rows;
      document.getElementById("total").textContent = cart.reduce((sum, dish) => sum + dish.price, 0).toFixed(2);
      document.querySelector("dialog").showModal();
    }

    function checkout() {
      if (!cart.length) return alert("Add something to your cart first!");
      alert("Thanks! This demo does not process real payments.");
    }
  </script>
</body>
</html>
