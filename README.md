<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Boutique Vêtements</title>
<style>
  body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #f5f5f5; }
  header { background: #333; color: white; padding: 1em; text-align: center; }
  main { max-width: 900px; margin: 2em auto; background: white; padding: 1em; border-radius: 8px; }
  h1, h2 { color: #333; }
  .product { border: 1px solid #ddd; padding: 1em; margin-bottom: 1em; border-radius: 5px; display: flex; }
  .product img { max-width: 150px; border-radius: 5px; }
  .details { margin-left: 1em; flex-grow: 1; }
  .price { font-weight: bold; color: #e91e63; margin-top: 0.5em; }
  button { background: #e91e63; color: white; border: none; padding: 0.5em 1em; cursor: pointer; border-radius: 3px; }
  button:hover { background: #c2185b; }
  #cart { position: fixed; top: 10px; right: 10px; background: white; border: 1px solid #ddd; padding: 1em; border-radius: 8px; width: 300px; max-height: 400px; overflow-y: auto; box-shadow: 0 0 10px rgba(0,0,0,0.2);}
  #cart h3 { margin-top: 0; }
  #cart ul { list-style: none; padding: 0; }
  #cart ul li { margin-bottom: 0.5em; }
  #cart button { background: #555; padding: 0.2em 0.5em; margin-left: 0.5em; font-size: 0.8em; }
</style>
</head>
<body>

<header>
  <h1>Boutique Vêtements</h1>
</header>

<main>
  <h2>Nos produits</h2>
  <div class="product" data-id="1" data-name="T-shirt blanc" data-price="15">
    <img src="https://via.placeholder.com/150?text=T-shirt+blanc" alt="T-shirt blanc" />
    <div class="details">
      <h3>T-shirt blanc</h3>
      <p>100% coton, disponible en tailles S, M, L.</p>
      <div class="price">15 €</div>
      <button onclick="addToCart(1)">Ajouter au panier</button>
    </div>
  </div>

  <div class="product" data-id="2" data-name="Sweat à capuche noir" data-price="35">
    <img src="https://via.placeholder.com/150?text=Sweat+noir" alt="Sweat à capuche noir" />
    <div class="details">
      <h3>Sweat à capuche noir</h3>
      <p>Chaud et confortable, tailles S à XL.</p>
      <div class="price">35 €</div>
      <button onclick="addToCart(2)">Ajouter au panier</button>
    </div>
  </div>

  <div class="product" data-id="3" data-name="Casquette rouge" data-price="12">
    <img src="https://via.placeholder.com/150?text=Casquette+rouge" alt="Casquette rouge" />
    <div class="details">
      <h3>Casquette rouge</h3>
      <p>Unisexe, taille unique, réglable.</p>
      <div class="price">12 €</div>
      <button onclick="addToCart(3)">Ajouter au panier</button>
    </div>
  </div>
</main>

<div id="cart">
  <h3>Panier</h3>
  <ul id="cart-items"></ul>
  <div><strong>Total : </strong><span id="total-price">0</span> €</div>
  <button onclick="checkout()">Commander</button>
</div>

<script>
  let cart = [];

  function addToCart(id) {
    const productElem = document.querySelector(`.product[data-id='${id}']`);
    const name = productElem.getAttribute('data-name');
    const price = parseFloat(productElem.getAttribute('data-price'));

    let found = cart.find(item => item.id === id);
    if (found) {
      found.qty++;
    } else {
      cart.push({ id, name, price, qty: 1 });
    }
    renderCart();
  }

  function renderCart() {
    const cartItems = document.getElementById('cart-items');
    cartItems.innerHTML = '';
    let total = 0;
    cart.forEach(item => {
      total += item.price * item.qty;
      let li = document.createElement('li');
      li.textContent = `${item.name} x${item.qty} - ${item.price * item.qty} €`;
      let btnRemove = document.createElement('button');
      btnRemove.textContent = '×';
      btnRemove.onclick = () => removeFromCart(item.id);
      li.appendChild(btnRemove);
      cartItems.appendChild(li);
    });
    document.getElementById('total-price').textContent = total.toFixed(2);
  }

  function removeFromCart(id) {
    cart = cart.filter(item => item.id !== id);
    renderCart();
  }

  function checkout() {
    if (cart.length === 0) {
      alert('Ton panier est vide !');
      return;
    }
    alert('Merci pour ta commande ! (Ceci est un prototype, pas de paiement réel)');
    cart = [];
    renderCart();
  }

  renderCart();
</script>

</body>
</html>
