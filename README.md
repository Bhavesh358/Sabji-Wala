import { useState } from "react"; import { ShoppingCart, Leaf } from "lucide-react"; import { Button } from "@/components/ui/button"; import { Card, CardContent } from "@/components/ui/card";

const products = [ { id: 1, name: "Aloo (Potato)", price: 30, unit: "kg", image: "https://i.imgur.com/4A1QdKX.png" }, { id: 2, name: "Tamatar (Tomato)", price: 40, unit: "kg", image: "https://i.imgur.com/7FzvJvE.png" }, { id: 3, name: "Pyaaz (Onion)", price: 25, unit: "kg", image: "https://i.imgur.com/jz3LgTf.png" }, { id: 4, name: "Bhindi (Lady Finger)", price: 50, unit: "kg", image: "https://i.imgur.com/1Ybkb7V.png" }, ];

export default function App() { const [cart, setCart] = useState([]);

const addToCart = (product) => { setCart([...cart, product]); };

const removeFromCart = (id) => { setCart(cart.filter((item, i) => i !== id)); };

const total = cart.reduce((sum, item) => sum + item.price, 0);

const orderNow = () => { let orderText = "Mera order hai:\n"; cart.forEach((item) => { orderText += - ${item.name} : ₹${item.price}/${item.unit}\n; }); orderText += Total: ₹${total};

const whatsappLink = `https://wa.me/91XXXXXXXXXX?text=${encodeURIComponent(orderText)}`;
window.open(whatsappLink, "_blank");

};

return ( <div className="min-h-screen bg-green-50 p-4"> <header className="flex justify-between items-center mb-6"> <h1 className="text-2xl font-bold flex items-center gap-2"> <Leaf className="text-green-600" /> Gaon Sabzi Bazar </h1> <div className="flex items-center gap-2"> <ShoppingCart /> <span>{cart.length}</span> </div> </header>

<div className="grid grid-cols-1 md:grid-cols-3 gap-4">
    {products.map((product) => (
      <Card key={product.id} className="rounded-2xl shadow-md">
        <CardContent className="p-4 flex flex-col items-center">
          <img src={product.image} alt={product.name} className="w-28 h-28 object-contain" />
          <h2 className="text-lg font-semibold mt-2">{product.name}</h2>
          <p className="text-gray-600">₹{product.price}/{product.unit}</p>
          <Button className="mt-2 w-full" onClick={() => addToCart(product)}>Add to Cart</Button>
        </CardContent>
      </Card>
    ))}
  </div>

  {cart.length > 0 && (
    <div className="mt-6 bg-white rounded-2xl shadow-md p-4">
      <h2 className="text-xl font-bold mb-2">🛒 Your Cart</h2>
      {cart.map((item, i) => (
        <div key={i} className="flex justify-between items-center border-b py-2">
          <span>{item.name}</span>
          <div className="flex gap-2 items-center">
            <span>₹{item.price}</span>
            <Button size="sm" variant="destructive" onClick={() => removeFromCart(i)}>Remove</Button>
          </div>
        </div>
      ))}
      <p className="font-semibold mt-2">Total: ₹{total}</p>
      <Button className="mt-4 w-full bg-green-600" onClick={orderNow}>Order on WhatsApp</Button>
    </div>
  )}
</div>

); }

