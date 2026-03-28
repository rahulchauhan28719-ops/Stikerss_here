# Stikerss_here
Come here<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sticker Shop - Cool Stickers Collection</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .header {
            text-align: center;
            padding: 2rem;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header h1 {
            font-size: 3rem;
            margin-bottom: 0.5rem;
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }

        .filters {
            display: flex;
            gap: 1rem;
            justify-content: center;
            margin-bottom: 2rem;
            flex-wrap: wrap;
        }

        .filter-btn {
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 50px;
            background: rgba(255,255,255,0.2);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .filter-btn:hover, .filter-btn.active {
            background: rgba(255,255,255,0.4);
            transform: translateY(-2px);
        }

        .sticker-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-bottom: 3rem;
        }

        .sticker-card {
            background: white;
            border-radius: 20px;
            padding: 1.5rem;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
            cursor: pointer;
        }

        .sticker-card:hover {
            transform: translateY(-10px) scale(1.02);
            box-shadow: 0 30px 60px rgba(0,0,0,0.2);
        }

        .sticker-image {
            width: 100%;
            height: 250px;
            object-fit: cover;
            border-radius: 15px;
            margin-bottom: 1rem;
            transition: transform 0.3s ease;
        }

        .sticker-card:hover .sticker-image {
            transform: scale(1.05);
        }

        .sticker-name {
            font-size: 1.4rem;
            font-weight: bold;
            margin-bottom: 0.5rem;
            color: #333;
        }

        .sticker-price {
            font-size: 1.2rem;
            color: #e74c3c;
            font-weight: bold;
        }

        .sticker-category {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: #ff6b6b;
            color: white;
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: bold;
        }

        .add-to-cart {
            width: 100%;
            padding: 0.8rem;
            background: linear-gradient(45deg, #ff6b6b, #ee5a24);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 1rem;
        }

        .add-to-cart:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 20px rgba(255,107,107,0.4);
        }

        .cart {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            background: white;
            padding: 1rem;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            min-width: 60px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .cart:hover {
            min-width: 200px;
            padding-right: 2rem;
        }

        .cart-count {
            background: #ff6b6b;
            color: white;
            border-radius: 50%;
            width: 25px;
            height: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9rem;
            font-weight: bold;
            margin-left: 0.5rem;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2rem;
            }
            .sticker-grid {
                grid-template-columns: 1fr;
            }
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>🎨 Sticker Shop</h1>
        <p>Find your perfect sticker to express yourself!</p>
    </div>

    <div class="container">
        <div class="filters">
            <button class="filter-btn active" data-category="all">All</button>
            <button class="filter-btn" data-category="animals">Animals</button>
            <button class="filter-btn" data-category="food">Food</button>
            <button class="filter-btn" data-category="tech">Tech</button>
            <button class="filter-btn" data-category="music">Music</button>
            <button class="filter-btn" data-category="gaming">Gaming</button>
        </div>

        <div class="sticker-grid" id="stickerGrid">
            <!-- Stickers will be populated by JavaScript -->
        </div>
    </div>

    <div class="cart" id="cartBtn">
        🛒 <span class="cart-count" id="cartCount">0</span>
    </div>

    <script>
        const stickers = [
            {
                id: 1,
                name: "Cute Cat",
                price: "$2.99",
                category: "animals",
                image: "https://images.unsplash.com/photo-1514888286974-6c03e2ca1dba?w=400&h=300&fit=crop"
            },
            {
                id: 2,
                name: "Pizza Slice",
                price: "$1.99",
                category: "food",
                image: "https://images.unsplash.com/photo-1513104890138-7c749659a591?w=400&h=300&fit=crop"
            },
            {
                id: 3,
                name: "Rocket Ship",
                price: "$3.49",
                category: "tech",
                image: "https://images.unsplash.com/photo-1579762718865-534b93618f42?w=400&h=300&fit=crop"
            },
            {
                id: 4,
                name: "Guitar Rock",
                price: "$2.49",
                category: "music",
                image: "https://images.unsplash.com/photo-1574535992097-2e0d8bb9c0a8?w=400&h=300&fit=crop"
            },
            {
                id: 5,
                name: "Game Controller",
                price: "$2.79",
                category: "gaming",
                image: "https://images.unsplash.com/photo-1612349317150-e413f6a5b16d?w=400&h=300&fit=crop"
            },
            {
                id: 6,
                name: "Happy Dog",
                price: "$2.29",
                category: "animals",
                image: "https://images.unsplash.com/photo-1543466835-00a7907e9de1?w=400&h=300&fit=crop"
            },
            {
                id: 7,
                name: "Ice Cream Cone",
                price: "$1.79",
                category: "food",
                image: "https://images.unsplash.com/photo-1562440499-64e1f146e1e6?w=400&h=300&fit=crop"
            },
            {
                id: 8,
                name: "Circuit Board",
                price: "$3.99",
                category: "tech",
                image: "https://images.unsplash.com/photo-1614751686944-0f9de72874ae?w=400&h=300&fit=crop"
            },
            {
                id: 9,
                name: "Headphones",
                price: "$2.99",
                category: "music",
                image: "https://images.unsplash.com/photo-1484704849700-f032a568e944?w=400&h=300&fit=crop"
            },
            {
                id: 10,
                name: "Pixel Heart",
                price: "$1.99",
                category: "gaming",
                image: "https://images.unsplash.com/photo-1544194215-398cb2c91517?w=400&h=300&fit=crop"
            },
            {
                id: 11,
                name: "Burger Time",
                price: "$2.19",
                category: "food",
                image: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=400&h=300&fit=crop"
            },
            {
                id: 12,
                name: "Robot Friend",
                price: "$4.49",
                category: "tech",
                image: "https://images.unsplash.com/photo-1518709268805-4e9042af2176?w=400&h=300&fit=crop"
            }
        ];

        let cartCount = 0;
        let currentFilter = 'all';

        function renderStickers(category = 'all') {
            const grid = document.getElementById('stickerGrid');
            const filteredStickers = category === 'all' ? stickers : stickers.filter(s => s.category === category);
            
            grid.innerHTML = filteredStickers.map(sticker => `
                <div class="sticker-card" data-category="${sticker.category}">
                    <div class="sticker-category">${sticker.category.toUpperCase()}</div>
                    <img src="${sticker.image}" alt="${sticker.name}" class="sticker-image">
                    <div class="sticker-name">${sticker.name}</div>
                    <div class="sticker-price">${sticker.price}</div>
                    <button class="add-to-cart" onclick="addToCart(${sticker.id})">
                        Add to Cart
                    </button>
                </div>
            `).join('');
        }

        function addToCart(id) {
            cartCount++;
            document.getElementById('cartCount').textContent = cartCount;
            
            // Add animation
            const btn = event.target;
            btn.textContent = 'Added! 🎉';
            btn.style.background = 'linear-gradient(45deg, #27ae60, #2ecc71)';
            
            setTimeout(() => {
                btn.textContent = 'Add to Cart';
                btn.style.background = 'linear-gradient(45deg, #ff6b6b, #ee5a24)';
            }, 1500);
        }

        // Filter functionality
        document.querySelectorAll('.filter-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                currentFilter = btn.dataset.category;
                renderStickers(currentFilter);
            });
        });

        // Cart button hover effect
        document.getElementById('cartBtn').addEventListener('mouseenter', function() {
            this.innerHTML = '🛒 Your Cart <span class="cart-count" id="cartCount">' + cartCount + '</span>';
        });
        

        document.getElementById('cartBtn').addEventListener('mouseleave', function() {
            this.innerHTML = '🛒 <span class="cart-count" id="cartCount">' + cartCount + '</span>';
        });

        // Initialize
        renderStickers();
    </script>
</body>
</html> and get some unique stickers.
