# ga-dona-menu
<script>
const products = [
  {id: 1, name: "Small Chips", price: 25},
  {id: 2, name: "Medium Chips", price: 30},
  {id: 3, name: "Large Chips", price: 35},
  {id: 4, name: "Extra Large Chips", price: 42},
  {id: 5, name: "2 Litre Flavoured Drink", price: 30},
  {id: 6, name: "2 Litre Coke", price: 33},
  {id: 7, name: "1.25 Litre Drink", price: 17},
  {id: 8, name: "1.5 Litre Cappy Juice", price: 40},
  {id: 9, name: "Coke Can", price: 15},
  {id: 10, name: "Cappy Can", price: 20},
  {id: 11, name: "Dry Lemon Can", price: 23},
  {id: 12, name: "Tonic Water Can", price: 23},
  {id: 13, name: "Egg", price: 5},
  {id: 14, name: "Vianna", price: 7},
  {id: 15, name: "Cheese", price: 5},
  {id: 16, name: "Polony", price: 5},
  {id: 17, name: "Russian", price: 15}
];

let cart = [];

function addToCart(id) {
  const product = products.find(p => p.id === id);
  const existing = cart.find(item => item.id === id);

  if (existing) {
    existing.quantity++;
  } else {
    cart.push({...product, quantity: 1});
  }

  showCart();
}

function changeQuantity(id, amount) {
  const item = cart.find(p => p.id === id);
  if (!item) return;

  item.quantity += amount;
  cart = cart.filter(p => p.quantity > 0);
  showCart();
}

function showCart() {
  const container = document.getElementById("cart");
  const total = cart.reduce(
    (sum, item) => sum + item.price * item.quantity, 0
  );

  container.innerHTML = cart.map(item => `
    <p>
      ${item.name} × ${item.quantity}
      — R${(item.price * item.quantity).toFixed(2)}
      <button onclick="changeQuantity(${item.id}, -1)">−</button>
      <button onclick="changeQuantity(${item.id}, 1)">+</button>
    </p>
  `).join("");

  container.innerHTML += `<h3>Total: R${total.toFixed(2)}</h3>`;
}
</script>
