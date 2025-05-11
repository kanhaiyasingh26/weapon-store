import React, { useState } from "react";

export default function App() {
  const [cart, setCart] = useState([]);
  const [activeCategory, setActiveCategory] = useState("All");
  const [searchTerm, setSearchTerm] = useState("");

  const weapons = [
    {
      id: 1,
      name: "Kilvish Shield",
      price: 299.99,
      category: "Defensive",
      image: "https://i.postimg.cc/KYLqgGXH/caeb8471-b390-4978-ba93-04d2539cdc03.png ",
    },
    {
      id: 2,
      name: "Khema Fire Shaft",
      price: 499.99,
      category: "Offensive",
      image: "https://i.postimg.cc/k5n6WsLP/41836533-5d9b-458a-a6bb-89c5ebe2c6fe.png ",
    },
    {
      id: 3,
      name: "Andhera Kayam Torch",
      price: 199.5,
      category: "Utility",
      image: "https://i.postimg.cc/ht0bFXBg/f00edccf-f085-4171-85c3-76d476b29ab1.png ",
    },
    {
      id: 4,
      name: "Pushpe Flower Bomb",
      price: 349.99,
      category: "Explosive",
      image: "https://i.postimg.cc/SKNLmmS9/972e5909-3d64-40f0-8465-0af89e85e4f1.png ",
    },
    {
      id: 5,
      name: "Kilvish Blackhole Door",
      price: 799.0,
      category: "Defensive",
      image: "https://i.postimg.cc/fLVx050T/dcb4b715-6a73-441a-8d46-e5a1e18b5136.png ",
    },
    {
      id: 6,
      name: "Khamsingh Laser Eyes",
      price: 899.99,
      category: "Offensive",
      image: "https://i.postimg.cc/76jS17g1/dd80152a-a281-49e6-9acd-e31e43e200e2.png ",
    },
    {
      id: 7,
      name: "Pushpe Mindcontrol Device",
      price: 599.99,
      category: "Utility",
      image: "https://i.postimg.cc/pr8zsTZw/17ac163c-9af7-43fd-9ef2-4ace3443ee1a.png ",
    },
  ];

  const categories = ["All", ...new Set(weapons.map((item) => item.category))];

  const filteredWeapons = weapons.filter(
    (item) =>
      (activeCategory === "All" || item.category === activeCategory) &&
      item.name.toLowerCase().includes(searchTerm.toLowerCase())
  );

  const addToCart = (item) => {
    setCart((prev) => [...prev, item]);
  };

  return (
    <div className="min-h-screen bg-gray-900 text-white">
      {/* Header */}
      <header className="bg-indigo-700 shadow-md sticky top-0 z-50">
        <div className="container mx-auto px-4 py-4 flex flex-col md:flex-row items-center justify-between gap-4">
          <h1 className="text-2xl font-bold tracking-tight">Weapon Arsenal</h1>
          <div className="w-full md:w-64 relative">
            <input
              type="text"
              placeholder="Search weapons..."
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              className="w-full pl-10 pr-4 py-2 rounded-full text-gray-800 focus:outline-none"
            />
            <svg
              className="absolute left-3 top-2.5 w-5 h-5 text-gray-500"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth={2}
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
              />
            </svg>
          </div>
          <div className="relative">
            <button className="flex items-center space-x-2 bg-white text-indigo-700 px-4 py-2 rounded-full hover:bg-indigo-50 transition">
              <svg
                className="w-5 h-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  strokeLinecap="round"
                  strokeLinejoin="round"
                  strokeWidth={2}
                  d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
                />
              </svg>
              <span>Cart ({cart.length})</span>
            </button>
            {cart.length > 0 && (
              <div className="absolute right-0 mt-2 w-64 max-h-96 overflow-y-auto bg-gray-800 rounded-lg shadow-xl p-2 animate-fade-in">
                {cart.map((item, index) => (
                  <div
                    key={index}
                    className="flex items-center justify-between p-2 border-b border-gray-700"
                  >
                    <p className="text-sm">{item.name}</p>
                    <p className="text-sm font-medium">${item.price.toFixed(2)}</p>
                  </div>
                ))}
                <div className="p-2 pt-3 flex justify-between font-semibold border-t border-gray-700">
                  <span>Total:</span>
                  <span>
                    $
                    {cart
                      .reduce((sum, item) => sum + item.price, 0)
                      .toFixed(2)}
                  </span>
                </div>
                <button className="mt-2 w-full bg-indigo-600 text-white py-2 rounded hover:bg-indigo-700 transition">
                  Checkout
                </button>
              </div>
            )}
          </div>
        </div>
      </header>

      {/* Categories */}
      <section className="py-4 bg-gray-800 sticky top-16 z-40 shadow-sm">
        <div className="container mx-auto px-4 overflow-x-auto flex space-x-4 pb-2">
          {categories.map((category, idx) => (
            <button
              key={idx}
              onClick={() => setActiveCategory(category)}
              className={`px-4 py-2 rounded-full whitespace-nowrap transition-all ${
                activeCategory === category
                  ? "bg-indigo-600 text-white"
                  : "bg-gray-700 text-gray-300 hover:bg-gray-600"
              }`}
            >
              {category}
            </button>
          ))}
        </div>
      </section>

      {/* Hero Section */}
      <section className="bg-gradient-to-r from-indigo-800 to-purple-900 py-12">
        <div className="container mx-auto px-4 flex flex-col md:flex-row items-center">
          <div className="md:w-1/2 mb-8 md:mb-0">
            <h2 className="text-3xl md:text-4xl font-bold mb-4 leading-tight">
              Ultimate Weapon Collection for Modern Warriors
            </h2>
            <p className="text-lg opacity-90 mb-6">
              Discover the most powerful and legendary weapons at unbeatable prices.
            </p>
            <button className="bg-indigo-600 text-white px-6 py-3 rounded-full font-semibold hover:bg-indigo-700 transition">
              Shop Now
            </button>
          </div>
          <div className="md:w-1/2 flex justify-center">
            <img
              src="https://i.postimg.cc/m23MFcCP/3d75e3bd-d460-4666-bff7-bce9d76713aa.png "
              alt="Weapons"
              className="rounded-lg shadow-lg transform hover:scale-105 transition duration-300"
            />
          </div>
        </div>
      </section>

      {/* Products Grid */}
      <main className="container mx-auto px-4 py-12">
        <h2 className="text-2xl font-bold mb-6 text-gray-200">
          {activeCategory === "All"
            ? "All Weapons"
            : `${activeCategory} Weapons`}
        </h2>
        {filteredWeapons.length === 0 ? (
          <div className="text-center py-12">
            <p className="text-gray-500 text-lg">No weapons found.</p>
          </div>
        ) : (
          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
            {filteredWeapons.map((item) => (
              <div
                key={item.id}
                className="bg-gray-800 rounded-lg shadow hover:shadow-xl transition-all overflow-hidden group"
              >
                <div className="aspect-w-3 aspect-h-2">
                  <img
                    src={item.image}
                    alt={item.name}
                    className="w-full h-48 object-cover transition-transform duration-500 group-hover:scale-105"
                  />
                </div>
                <div className="p-4">
                  <div className="flex justify-between items-start mb-2">
                    <h3 className="font-semibold text-lg">{item.name}</h3>
                    <span className="bg-indigo-100 text-indigo-800 text-xs font-semibold px-2 py-1 rounded">
                      {item.category}
                    </span>
                  </div>
                  <p className="text-indigo-400 font-bold mb-3">${item.price.toFixed(2)}</p>
                  <button
                    onClick={() => addToCart(item)}
                    className="w-full bg-indigo-600 text-white py-2 rounded hover:bg-indigo-700 transition flex items-center justify-center space-x-2"
                  >
                    <svg
                      className="w-5 h-5"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path
                        strokeLinecap="round"
                        strokeLinejoin="round"
                        strokeWidth={2}
                        d="M12 6v6m0 0v6m0-6h6m-6 0H6"
                      />
                    </svg>
                    <span>Add to Cart</span>
                  </button>
                </div>
              </div>
            ))}
          </div>
        )}
      </main>

      {/* Features Section */}
      <section className="bg-gray-800 py-12">
        <div className="container mx-auto px-4">
          <h2 className="text-2xl font-bold text-center mb-10 text-gray-200">
            Why Choose Our Arsenal?
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
            <div className="bg-gray-700 p-6 rounded-lg shadow text-center">
              <div className="w-16 h-16 mx-auto mb-4 flex items-center justify-center bg-indigo-100 text-indigo-700 rounded-full">
                <svg
                  className="w-8 h-8"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    strokeLinecap="round"
                    strokeLinejoin="round"
                    strokeWidth={2}
                    d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"
                  />
                </svg>
              </div>
              <h3 className="text-xl font-semibold mb-2">Legendary Quality</h3>
              <p className="text-gray-400">
                Each weapon is forged with ancient power and tested for battle readiness.
              </p>
            </div>
            <div className="bg-gray-700 p-6 rounded-lg shadow text-center">
              <div className="w-16 h-16 mx-auto mb-4 flex items-center justify-center bg-indigo-100 text-indigo-700 rounded-full">
                <svg
                  className="w-8 h-8"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    strokeLinecap="round"
                    strokeLinejoin="round"
                    strokeWidth={2}
                    d="M13 10V3L4 14h7v7l9-11h-7z"
                  />
                </svg>
              </div>
              <h3 className="text-xl font-semibold mb-2">Fast Delivery</h3>
              <p className="text-gray-400">
                Get your weapons delivered within hours using our interdimensional transport system.
              </p>
            </div>
            <div className="bg-gray-700 p-6 rounded-lg shadow text-center">
              <div className="w-16 h-16 mx-auto mb-4 flex items-center justify-center bg-indigo-100 text-indigo-700 rounded-full">
                <svg
                  className="w-8 h-8"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    strokeLinecap="round"
                    strokeLinejoin="round"
                    strokeWidth={2}
                    d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                  />
                </svg>
              </div>
              <h3 className="text-xl font-semibold mb-2">Epic Deals</h3>
              <p className="text-gray-400">
                Legendary power doesn't have to cost a kingdom - get great deals daily!
              </p>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-900 text-gray-400 py-10 mt-12">
        <div className="container mx-auto px-4">
          <div className="flex flex-col md:flex-row justify-between">
            <div className="mb-6 md:mb-0">
              <h3 className="text-xl font-bold mb-2 text-white">Weapon Arsenal</h3>
              <p className="max-w-xs">
                The ultimate arsenal for warriors of all realms. Powerful weapons, instant delivery.
              </p>
            </div>
            <div>
              <h3 className="text-lg font-semibold mb-4 text-white">Quick Links</h3>
              <ul className="space-y-2">
                <li>
                  <a href="#" className="hover:text-white transition">
                    Home
                  </a>
                </li>
                <li>
                  <a href="#" className="hover:text-white transition">
                    Shop
                  </a>
                </li>
                <li>
                  <a href="#" className="hover:text-white transition">
                    About Us
                  </a>
                </li>
                <li>
                  <a href="#" className="hover:text-white transition">
                    Contact
                  </a>
                </li>
              </ul>
            </div>
          </div>
          <div className="border-t border-gray-700 mt-8 pt-6 text-center">
            <p>&copy; {new Date().getFullYear()} Weapon Arsenal. All rights reserved.</p>
          </div>
        </div>
      </footer>
    </div>
  );
}