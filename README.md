import React, { useState } from 'react';
import { motion } from 'framer-motion';
import { ShoppingCart, Heart, LogIn, CreditCard, MessageCircle } from 'lucide-react';

export default function App() {
  const [cart, setCart] = useState([]);
  const [view, setView] = useState('home');

  const products = [
    { id: 1, name: 'Lubrificante Íntimo Premium', price: 59.90, image: 'https://via.placeholder.com/300x300?text=Lubrificante' },
    { id: 2, name: 'Vibrador Clitoriano Lux', price: 199.90, image: 'https://via.placeholder.com/300x300?text=Vibrador' },
    { id: 3, name: 'Kit Sensual Couple', price: 149.90, image: 'https://via.placeholder.com/300x300?text=Kit+Sensual' }
  ];

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  const checkoutTotal = cart.reduce((acc, p) => acc + p.price, 0);

  return (
    <div className="min-h-screen bg-black text-white font-sans">
      {/* Header */}
      <header className="flex justify-between items-center p-6 border-b border-gray-800">
        <h1 className="text-3xl font-serif text-[#d4af37]">Intimacy Love</h1>
        <div className="flex items-center gap-6">
          <button onClick={() => setView('home')} className="hover:text-[#d4af37]">Home</button>
          <button onClick={() => setView('blog')} className="hover:text-[#d4af37]">Blog</button>
          <button onClick={() => setView('sobre')} className="hover:text-[#d4af37]">Sobre</button>
          <button onClick={() => setView('cart')} className="relative">
            <ShoppingCart />
            {cart.length > 0 && (
              <span className="absolute -top-2 -right-2 bg-[#d4af37] text-black rounded-full text-xs px-1">{cart.length}</span>
            )}
          </button>
        </div>
      </header>

      {/* Views */}
      {view === 'home' && (
        <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} className="p-8 grid md:grid-cols-3 gap-8">
          {products.map((p) => (
            <div key={p.id} className="bg-[#111] p-4 rounded-2xl shadow-lg border border-gray-800 hover:border-[#d4af37] transition">
              <img src={p.image} alt={p.name} className="rounded-xl mb-4" />
              <h2 className="text-xl mb-2">{p.name}</h2>
              <p className="text-[#d4af37] mb-4">R$ {p.price.toFixed(2)}</p>
              <button onClick={() => addToCart(p)} className="bg-[#d4af37] text-black px-4 py-2 rounded-xl hover:bg-[#b8962e] transition">Adicionar ao Carrinho</button>
            </div>
          ))}
        </motion.section>
      )}

      {view === 'cart' && (
        <motion.section initial={{ x: 50, opacity: 0 }} animate={{ x: 0, opacity: 1 }} className="p-8">
          <h2 className="text-2xl mb-6">Seu Carrinho</h2>
          {cart.length === 0 ? (
            <p>Seu carrinho está vazio.</p>
          ) : (
            <div>
              {cart.map((item, i) => (
                <div key={i} className="flex justify-between border-b border-gray-800 py-3">
                  <span>{item.name}</span>
                  <span>R$ {item.price.toFixed(2)}</span>
                </div>
              ))}
              <div className="mt-6 text-lg">Total: <span className="text-[#d4af37]">R$ {checkoutTotal.toFixed(2)}</span></div>
              <button onClick={() => setView('checkout')} className="mt-4 bg-[#d4af37] text-black px-6 py-2 rounded-xl">Finalizar Compra</button>
            </div>
          )}
        </motion.section>
      )}

      {view === 'checkout' && (
        <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} className="p-8">
          <h2 className="text-2xl mb-4">Checkout</h2>
          <p className="mb-4">Selecione o método de pagamento simulado:</p>
          <div className="flex gap-4">
            <button className="bg-[#d4af37] text-black px-6 py-3 rounded-xl flex items-center gap-2"><CreditCard /> Cartão</button>
            <button className="bg-[#d4af37] text-black px-6 py-3 rounded-xl flex items-center gap-2">PIX</button>
          </div>
          <p className="mt-6 text-gray-400">Simulação de pagamento — Nenhum dado real é processado.</p>
        </motion.section>
      )}

      {view === 'blog' && (
        <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} className="p-8 max-w-3xl mx-auto">
          <h2 className="text-3xl mb-6 text-[#d4af37]">Dicas & Prazer</h2>
          <article className="mb-6">
            <h3 className="text-xl mb-2">Como escolher o lubrificante ideal</h3>
            <p className="text-gray-400">Os lubrificantes melhoram o conforto e o prazer. Prefira à base de água para uso geral e à base de silicone para experiências prolongadas...</p>
          </article>
          <article>
            <h3 className="text-xl mb-2">A importância da conexão no relacionamento</h3>
            <p className="text-gray-400">O prazer vai além do físico: o vínculo emocional e a comunicação são essenciais para uma vida íntima plena...</p>
          </article>
        </motion.section>
      )}

      {view === 'sobre' && (
        <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} className="p-8 max-w-3xl mx-auto text-center">
          <h2 className="text-3xl mb-6 text-[#d4af37]">Sobre a Intimacy Love</h2>
          <p className="text-gray-400 mb-4">A Intimacy Love nasceu para celebrar o prazer com elegância e respeito. Nossa missão é oferecer produtos de qualidade premium, preservando a privacidade e promovendo o bem-estar.</p>
          <p className="text-gray-400">Atendimento personalizado, entrega discreta e uma curadoria feita com amor e sofisticação.</p>
        </motion.section>
      )}

      {/* WhatsApp Button */}
      <a href="https://wa.me/5599999999999" target="_blank" rel="noopener noreferrer" className="fixed bottom-6 right-6 bg-[#d4af37] text-black p-4 rounded-full shadow-lg hover:bg-[#b8962e] transition">
        <MessageCircle />
      </a>

      {/* Footer */}
      <footer className="p-6 border-t border-gray-800 text-center text-gray-500 text-sm mt-12">
        © 2025 Intimacy Love — Todos os direitos reservados.
      </footer>
    </div>
  );
}
