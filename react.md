/* React Router Navbar (React + Tailwind)

Files combined into a single preview for convenience. Copy each section into the matching file in a React project (create-react-app or Vite).

Requirements:

React 18+

react-router-dom v6+

TailwindCSS installed and configured (or replace Tailwind classes with your own CSS)


Commands to install dependencies (example using npm): npm install react-router-dom npm install -D tailwindcss postcss autoprefixer npx tailwindcss init -p

Tailwind sample config and index.css import are referenced below.


---

*/

// ---------- src/index.js ---------- import React from "react"; import { createRoot } from "react-dom/client"; import { BrowserRouter } from "react-router-dom"; import App from "./App"; import "./index.css"; // make sure Tailwind or your CSS is imported

const root = createRoot(document.getElementById("root")); root.render( <React.StrictMode> <BrowserRouter> <App /> </BrowserRouter> </React.StrictMode> );

// ---------- src/App.jsx ---------- import React from "react"; import { Routes, Route } from "react-router-dom"; import Navbar from "./components/Navbar"; import Home from "./pages/Home"; import About from "./pages/About"; import Products from "./pages/Products"; import Phones from "./pages/Phones"; import Laptops from "./pages/Laptops"; import NotFound from "./pages/NotFound";

export default function App() { return ( <div className="min-h-screen bg-gray-50"> <Navbar /> <main className="p-6"> <Routes> <Route path="/" element={<Home />} /> <Route path="/about" element={<About />} />

{/* Nested routes under /products */}
      <Route path="/products" element={<Products />}>
        <Route path="phones" element={<Phones />} />
        <Route path="laptops" element={<Laptops />} />
      </Route>

      <Route path="*" element={<NotFound />} />
    </Routes>
  </main>
</div>

); }

// ---------- src/components/Navbar.jsx ---------- import React, { useState } from "react"; import { NavLink, Link } from "react-router-dom";

function NavItem({ to, children, onClick }) { // NavLink provides an isActive boolean we can use to style the active link return ( <NavLink to={to} onClick={onClick} className={({ isActive }) => px-3 py-2 rounded-md text-sm font-medium transition-colors ${ isActive ? "bg-blue-600 text-white" : "text-gray-700 hover:bg-gray-200" } } > {children} </NavLink> ); }

export default function Navbar() { const [open, setOpen] = useState(false);

return ( <nav className="bg-white shadow"> <div className="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8"> <div className="flex h-16 items-center justify-between"> {/* Brand */} <div className="flex items-center"> <Link to="/" className="text-xl font-bold text-blue-600"> MyBrand </Link> <div className="hidden md:block md:ml-6"> <div className="flex items-center space-x-2"> <NavItem to="/">Home</NavItem> <NavItem to="/about">About</NavItem> <NavItem to="/products">Products</NavItem> </div> </div> </div>

{/* Mobile menu button */}
      <div className="-mr-2 flex md:hidden">
        <button
          onClick={() => setOpen((s) => !s)}
          aria-label="Toggle menu"
          className="inline-flex items-center justify-center rounded-md p-2 text-gray-700 hover:bg-gray-200"
        >
          {open ? (
            // Close icon
            <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          ) : (
            // Hamburger icon
            <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          )}
        </button>
      </div>

      {/* Desktop right side - example profile area (optional) */}
      <div className="hidden md:block">
        <div className="ml-4 flex items-center md:ml-6">
          <Link to="/" className="rounded-full bg-gray-100 px-3 py-1 text-sm font-medium text-gray-700">
            Sign in
          </Link>
        </div>
      </div>
    </div>
  </div>

  {/* Mobile menu (toggle) */}
  {open && (
    <div className="md:hidden">
      <div className="space-y-1 px-2 pt-2 pb-3">
        <NavItem to="/" onClick={() => setOpen(false)}>
          Home
        </NavItem>
        <NavItem to="/about" onClick={() => setOpen(false)}>
          About
        </NavItem>
        <NavItem to="/products" onClick={() => setOpen(false)}>
          Products
        </NavItem>
      </div>
    </div>
  )}
</nav>

); }

// ---------- src/pages/Home.jsx ---------- import React from "react";

export default function Home() { return ( <div> <h1 className="text-2xl font-bold">Home</h1> <p className="mt-2 text-gray-700">Welcome to the home page.</p> </div> ); }

// ---------- src/pages/About.jsx ---------- import React from "react";

export default function About() { return ( <div> <h1 className="text-2xl font-bold">About</h1> <p className="mt-2 text-gray-700">This is an example app with a responsive navbar using React Router.</p> </div> ); }

// ---------- src/pages/Products.jsx ---------- import React from "react"; import { Link, Outlet } from "react-router-dom";

export default function Products() { return ( <div> <h1 className="text-2xl font-bold">Products</h1> <p className="mt-2 text-gray-700">Choose a category:</p>

<nav className="mt-4 flex space-x-3">
    <Link to="phones" className="rounded-md px-3 py-1 text-sm font-medium bg-gray-100 hover:bg-gray-200">
      Phones
    </Link>
    <Link to="laptops" className="rounded-md px-3 py-1 text-sm font-medium bg-gray-100 hover:bg-gray-200">
      Laptops
    </Link>
  </nav>

  <div className="mt-6">
    <Outlet /> {/* Nested route content appears here */}
  </div>
</div>

); }

// ---------- src/pages/Phones.jsx ---------- import React from "react";

export default function Phones() { return ( <div> <h2 className="text-xl font-semibold">Phones</h2> <p className="mt-2 text-gray-700">List of phones would appear here.</p> </div> ); }

// ---------- src/pages/Laptops.jsx ---------- import React from "react";

export default function Laptops() { return ( <div> <h2 className="text-xl font-semibold">Laptops</h2> <p className="mt-2 text-gray-700">List of laptops would appear here.</p> </div> ); }

// ---------- src/pages/NotFound.jsx ---------- import React from "react";

export default function NotFound() { return ( <div> <h1 className="text-2xl font-bold">404 - Not Found</h1> <p className="mt-2 text-gray-700">The page you requested does not exist.</p> </div> ); }

// ---------- src/index.css (Tailwind minimal example) ---------- /* @tailwind base; @tailwind components; @tailwind utilities;

If you don't use Tailwind, add your own CSS or simple resets here. */