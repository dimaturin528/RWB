<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Маркетплейс | Твои товары</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: system-ui, 'Segoe UI', 'Inter', -apple-system, BlinkMacSystemFont, 'Roboto', sans-serif;
        }

        body {
            background: #f4f6fa;
            padding: 2rem 1.5rem;
            color: #1a1f2e;
        }

        /* контейнер */
        .marketplace {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* шапка */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 2rem;
            padding-bottom: 1rem;
            border-bottom: 2px solid #e2e8f0;
        }

        .logo h1 {
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(135deg, #1e2b3c, #2c5f7a);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: -0.3px;
        }

        .logo p {
            font-size: 0.85rem;
            color: #4a5b6e;
            margin-top: 4px;
        }

        .cart-info {
            background: white;
            padding: 0.6rem 1.2rem;
            border-radius: 60px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.02), 0 1px 2px rgba(0, 0, 0, 0.05);
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 1px solid #e2edf2;
        }

        .cart-info:hover {
            background: #fef9e8;
            border-color: #ffcd7e;
            transform: scale(0.98);
        }

        .cart-icon {
            font-size: 1.4rem;
        }

        .cart-count {
            background: #2c5f7a;
            color: white;
            border-radius: 40px;
            padding: 2px 10px;
            font-size: 0.85rem;
            font-weight: 600;
        }

        /* сетка товаров */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
            gap: 1.8rem;
            margin: 2rem 0 3rem;
        }

        /* карточка */
        .product-card {
            background: white;
            border-radius: 28px;
            overflow: hidden;
            box-shadow: 0 12px 24px -12px rgba(0, 0, 0, 0.1);
            transition: all 0.25s ease;
            cursor: pointer;
            border: 1px solid #eef2f8;
            display: flex;
            flex-direction: column;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 24px 32px -16px rgba(0, 0, 0, 0.15);
            border-color: #cbdde9;
        }

        /* область изображения (заглушка, но можно подставить картинку) */
        .product-img {
            background: #eef3fc;
            height: 180px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            font-weight: 400;
            color: #2c5f7a;
            border-bottom: 1px solid #e6edf4;
        }

        .product-info {
            padding: 1rem 1.2rem 1.2rem;
            flex: 1;
        }

        .product-title {
            font-size: 1.25rem;
            font-weight: 600;
            margin-bottom: 0.5rem;
            line-height: 1.3;
            display: flex;
            justify-content: space-between;
            align-items: start;
        }

        .product-price {
            font-size: 1.35rem;
            font-weight: 700;
            color: #1f5e7e;
            margin: 0.5rem 0 0.6rem;
        }

        .product-price small {
            font-size: 0.8rem;
            font-weight: 400;
            color: #6c7e94;
        }

        .product-desc {
            font-size: 0.85rem;
            color: #4f5f73;
            margin-bottom: 1rem;
            line-height: 1.4;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
        }

        /* кнопка добавления (кликабельный элемент внутри карточки) */
        .add-to-cart-btn {
            background: #f0f4f9;
            border: none;
            width: 100%;
            padding: 10px 0;
            border-radius: 40px;
            font-weight: 600;
            font-size: 0.9rem;
            color: #1e2f3c;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            margin-top: 8px;
        }

        .add-to-cart-btn:hover {
            background: #2c5f7a;
            color: white;
        }

        /* корзина (боковая панель) — модальное окно */
        .cart-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(4px);
            justify-content: flex-end;
            z-index: 1000;
        }

        .cart-panel {
            background: white;
            width: 100%;
            max-width: 420px;
            height: 100%;
            overflow-y: auto;
            padding: 1.5rem;
            box-shadow: -8px 0 30px rgba(0, 0, 0, 0.2);
            display: flex;
            flex-direction: column;
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid #e9edf2;
            padding-bottom: 1rem;
            margin-bottom: 1.2rem;
            font-size: 1.4rem;
            font-weight: 700;
        }

        .close-cart {
            background: none;
            border: none;
            font-size: 1.8rem;
            cursor: pointer;
            line-height: 1;
            padding: 0 8px;
            border-radius: 30px;
        }

        .cart-items-list {
            flex: 1;
            list-style: none;
            margin-bottom: 1.5rem;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.8rem 0;
            border-bottom: 1px solid #eef2f8;
            gap: 12px;
        }

        .cart-item-info {
            flex: 2;
        }

        .cart-item-title {
            font-weight: 500;
            font-size: 0.95rem;
        }

        .cart-item-price {
            font-size: 0.85rem;
            color: #2c5f7a;
            font-weight: 500;
        }

        .cart-item-remove {
            background: #fee2e2;
            border: none;
            border-radius: 40px;
            padding: 5px 12px;
            font-size: 0.75rem;
            cursor: pointer;
            font-weight: 500;
            color: #b91c1c;
            transition: 0.1s;
        }

        .cart-total {
            border-top: 2px dashed #dce5ec;
            padding-top: 1rem;
            font-size: 1.3rem;
            font-weight: 800;
            display: flex;
            justify-content: space-between;
            margin-top: 1rem;
        }

        .checkout-btn {
            background: #2c5f7a;
            color: white;
            border: none;
            padding: 14px;
            border-radius: 60px;
            font-weight: 700;
            font-size: 1rem;
            margin-top: 1.2rem;
            cursor: pointer;
            transition: 0.2s;
        }

        .empty-cart {
            text-align: center;
            padding: 2rem;
            color: #8e9eaf;
        }

        /* инструкция для быстрого редактирования */
        .editor-note {
            background: #fdf8e7;
            border-left: 4px solid #f3b33d;
            padding: 1rem 1.2rem;
            border-radius: 20px;
            font-size: 0.85rem;
            color: #7a6700;
            margin: 30px 0 10px;
        }

        button {
            background: none;
            border: none;
        }

        footer {
            margin-top: 2rem;
            font-size: 0.75rem;
            text-align: center;
            color: #8a99aa;
        }
    </style>
</head>
<body>
<div class="marketplace">
    <div class="header">
        <div class="logo">
            <h1>🛍️ Маркетплейс</h1>
            <p>кликай на товар или кнопку → в корзину</p>
        </div>
        <div class="cart-info" id="cartButton">
            <span class="cart-icon">🛒</span>
            <span>Корзина</span>
            <span class="cart-count" id="cartCount">0</span>
        </div>
    </div>

    <div class="products-grid" id="productsGrid">
        <!-- все карточки будут вставлены из JS, но чтобы ты сразу видел структуру и мог сам править товары — сделаем динамический рендер из данных -->
    </div>

    <div class="editor-note">
        ✏️ <strong>Как менять товары?</strong><br>
        Открой этот файл в редакторе, найди в коде переменную <code>productsData</code> (в разделе script).<br>
        Изменяй названия, цены, описание, эмодзи картинок — и всё обновится автоматически. Товары кликабельны!
    </div>
    <footer>
        ⚡ Нажми на карточку или на кнопку «В корзину» — товар добавится
    </footer>
</div>

<!-- Модалка корзины -->
<div id="cartModal" class="cart-modal">
    <div class="cart-panel">
        <div class="cart-header">
            🧺 Моя корзина
            <button class="close-cart" id="closeCartBtn">&times;</button>
        </div>
        <ul class="cart-items-list" id="cartItemsList">
            <li class="empty-cart">Корзина пуста</li>
        </ul>
        <div class="cart-total" id="cartTotal">
            <span>Итого:</span>
            <span>0 ₽</span>
        </div>
        <button class="checkout-btn" id="checkoutBtn">💳 Оформить заказ</button>
    </div>
</div>

<script>
    // ======================   ТВОИ ТОВАРЫ (меняй здесь!) ====================
    const productsData = [
        {
            id: 1,
            title: "Беспроводные наушники AirPods Pro",
            price: 18990,
            desc: "Активное шумоподавление, адаптивный эквалайзер, прозрачный режим.",
            imageEmoji: "🎧",
            bgColor: "#eef0fc"
        },
        {
            id: 2,
            title: "Смарт-часы Ultra 8",
            price: 27990,
            desc: "Отслеживание здоровья, GPS, шагомер, водонепроницаемый корпус.",
            imageEmoji: "⌚",
            bgColor: "#eefaf2"
        },
        {
            id: 3,
            title: "Игровая клавиатура RGB",
            price: 5490,
            desc: "Механические переключатели, подсветка, антипризраковая защита.",
            imageEmoji: "⌨️",
            bgColor: "#fef4e8"
        },
        {
            id: 4,
            title: "Рюкзак городской 20л",
            price: 3490,
            desc: "Водоотталкивающая ткань, отделение для ноутбука до 15.6 дюймов.",
            imageEmoji: "🎒",
            bgColor: "#e9f3fe"
        },
        {
            id: 5,
            title: "Умная колонка Voice",
            price: 7990,
            desc: "Голосовой помощник, стереозвук, управление умным домом.",
            imageEmoji: "🔊",
            bgColor: "#fceef5"
        },
        {
            id: 6,
            title: "Фитнес-браслет Band 6",
            price: 2690,
            desc: "Шагомер, пульсоксиметр, мониторинг сна, 7 дней работы.",
            imageEmoji: "⌚",
            bgColor: "#eaf7fa"
        },
        {
            id: 7,
            title: "Настольная лампа LED CCT",
            price: 2190,
            desc: "Регулировка яркости и оттенка, поворотная конструкция.",
            imageEmoji: "💡",
            bgColor: "#fff3e0"
        },
        {
            id: 8,
            title: "Пауэрбанк 20000mAh",
            price: 3290,
            desc: "Быстрая зарядка, 2 порта USB, цифровой индикатор.",
            imageEmoji: "🔋",
            bgColor: "#eef2fa"
        }
    ];
    // =================================================================

    // Состояние корзины: { id, title, price, quantity } (храним кол-во)
    let cart = [];

    // DOM элементы
    const productsGrid = document.getElementById("productsGrid");
    const cartModal = document.getElementById("cartModal");
    const cartButton = document.getElementById("cartButton");
    const closeCartBtn = document.getElementById("closeCartBtn");
    const cartItemsList = document.getElementById("cartItemsList");
    const cartCountSpan = document.getElementById("cartCount");
    const cartTotalSpan = document.querySelector("#cartTotal span:last-child");
    const checkoutBtn = document.getElementById("checkoutBtn");

    // Функция обновления отображения корзины (список, итог, счетчик)
    function updateCartUI() {
        // обновить счетчик в шапке
        const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
        cartCountSpan.innerText = totalItems;

        // отрисовать список в модалке
        if (!cartItemsList) return;
        if (cart.length === 0) {
            cartItemsList.innerHTML = '<li class="empty-cart">📭 Корзина пуста, добавьте товары</li>';
            cartTotalSpan.innerText = "0 ₽";
            return;
        }

        let html = "";
        let totalSum = 0;
        cart.forEach(item => {
            const itemTotal = item.price * item.quantity;
            totalSum += itemTotal;
            html += `
                <li class="cart-item" data-id="${item.id}">
                    <div class="cart-item-info">
                        <div class="cart-item-title">${escapeHtml(item.title)}</div>
                        <div class="cart-item-price">${item.price} ₽  × ${item.quantity} = ${itemTotal} ₽</div>
                    </div>
                    <button class="cart-item-remove" data-id="${item.id}">Удалить</button>
                </li>
            `;
        });
        cartItemsList.innerHTML = html;
        cartTotalSpan.innerText = totalSum.toLocaleString() + " ₽";

        // навесить обработчики на кнопки удаления
        document.querySelectorAll(".cart-item-remove").forEach(btn => {
            btn.addEventListener("click", (e) => {
                e.stopPropagation();
                const id = parseInt(btn.getAttribute("data-id"));
                removeFromCart(id);
            });
        });
    }

    // Добавить товар в корзину (или увеличить кол-во)
    function addToCart(product) {
        const existing = cart.find(item => item.id === product.id);
        if (existing) {
            existing.quantity += 1;
        } else {
            cart.push({
                id: product.id,
                title: product.title,
                price: product.price,
                quantity: 1
            });
        }
        updateCartUI();
        // визуальный фидбек - легкое подсвечивание корзины
        const cartElem = document.getElementById("cartButton");
        if (cartElem) {
            cartElem.style.transform = "scale(1.02)";
            setTimeout(() => { if(cartElem) cartElem.style.transform = ""; }, 150);
        }
    }

    // Удалить товар полностью из корзины
    function removeFromCart(productId) {
        cart = cart.filter(item => item.id !== productId);
        updateCartUI();
        if (cart.length === 0 && cartModal.style.display === "flex") {
            // обновить пустую строку
        }
    }

    // Вспомогательная функция для защиты от XSS
    function escapeHtml(str) {
        return str.replace(/[&<>]/g, function(m) {
            if (m === '&') return '&amp;';
            if (m === '<') return '&lt;';
            if (m === '>') return '&gt;';
            return m;
        }).replace(/[\uD800-\uDBFF][\uDC00-\uDFFF]/g, function(c) {
            return c;
        });
    }

    // рендерим карточки товаров
    function renderProducts() {
        if (!productsGrid) return;
        productsGrid.innerHTML = "";
        productsData.forEach(product => {
            const card = document.createElement("div");
            card.className = "product-card";
            // клик по карточке тоже добавляет в корзину (удобно)
            card.addEventListener("click", (e) => {
                // если клик был по кнопке, не дублируем (чтобы не вызывать дважды)
                if (e.target.classList && e.target.classList.contains("add-to-cart-btn")) {
                    return;
                }
                addToCart(product);
                showToast(`➕ ${product.title} добавлен`);
            });

            // область с эмодзи (вместо картинки)
            const imgDiv = document.createElement("div");
            imgDiv.className = "product-img";
            imgDiv.style.backgroundColor = product.bgColor || "#eef3fc";
            imgDiv.style.fontSize = "4rem";
            imgDiv.innerText = product.imageEmoji || "📦";
            
            const infoDiv = document.createElement("div");
            infoDiv.className = "product-info";
            
            const titleDiv = document.createElement("div");
            titleDiv.className = "product-title";
            titleDiv.innerHTML = `<span>${escapeHtml(product.title)}</span>`;
            
            const priceDiv = document.createElement("div");
            priceDiv.className = "product-price";
            priceDiv.innerHTML = `${product.price.toLocaleString()} <small>₽</small>`;
            
            const descDiv = document.createElement("div");
            descDiv.className = "product-desc";
            descDiv.innerText = product.desc;
            
            const addButton = document.createElement("button");
            addButton.className = "add-to-cart-btn";
            addButton.innerHTML = "🛒 В корзину";
            addButton.addEventListener("click", (e) => {
                e.stopPropagation();   // не даём карточке обработать повторно
                addToCart(product);
                showToast(`✅ ${product.title} в корзине`);
            });
            
            infoDiv.appendChild(titleDiv);
            infoDiv.appendChild(priceDiv);
            infoDiv.appendChild(descDiv);
            infoDiv.appendChild(addButton);
            card.appendChild(imgDiv);
            card.appendChild(infoDiv);
            productsGrid.appendChild(card);
        });
    }

    // простой тост (уведомление)
    let toastTimeout;
    function showToast(message) {
        let existingToast = document.querySelector(".custom-toast");
        if(existingToast) existingToast.remove();
        const toast = document.createElement("div");
        toast.className = "custom-toast";
        toast.innerText = message;
        toast.style.position = "fixed";
        toast.style.bottom = "24px";
        toast.style.left = "50%";
        toast.style.transform = "translateX(-50%)";
        toast.style.backgroundColor = "#1e2b3c";
        toast.style.color = "white";
        toast.style.padding = "10px 20px";
        toast.style.borderRadius = "50px";
        toast.style.fontSize = "0.9rem";
        toast.style.zIndex = "1100";
        toast.style.boxShadow = "0 4px 12px rgba(0,0,0,0.2)";
        toast.style.fontWeight = "500";
        toast.style.backdropFilter = "blur(4px)";
        document.body.appendChild(toast);
        if(toastTimeout) clearTimeout(toastTimeout);
        toastTimeout = setTimeout(() => {
            if(toast) toast.remove();
        }, 1800);
    }

    // модалка корзины
    function openCart() {
        updateCartUI();
        cartModal.style.display = "flex";
        document.body.style.overflow = "hidden";
    }
    function closeCart() {
        cartModal.style.display = "none";
        document.body.style.overflow = "";
    }

    // оформление заказа
    function handleCheckout() {
        if (cart.length === 0) {
            showToast("Корзина пуста, добавьте товары 😢");
            return;
        }
        const totalItems = cart.reduce((sum, i) => sum + i.quantity, 0);
        const totalPrice = cart.reduce((sum, i) => sum + (i.price * i.quantity), 0);
        alert(`🎉 Спасибо за заказ!\n📦 Товаров: ${totalItems} шт.\n💰 Сумма: ${totalPrice.toLocaleString()} ₽\n(демо-режим, заказ не отправлен)`);
        // очищаем корзину после заказа (как вариант)
        cart = [];
        updateCartUI();
        closeCart();
        showToast("✨ Корзина очищена, спасибо за покупку!");
    }

    // Добавляем обработчики событий
    cartButton.addEventListener("click", openCart);
    closeCartBtn.addEventListener("click", closeCart);
    checkoutBtn.addEventListener("click", handleCheckout);
    window.addEventListener("click", (e) => {
        if (e.target === cartModal) {
            closeCart();
        }
    });

    // инициализация
    renderProducts();
    updateCartUI();

    // небольшой фикс для динамических данных: корзина уже готова
    console.log("Маркетплейс готов! Товары кликабельны. Меняй массив productsData в коде :)");
</script>

<style>
    /* стиль для тоста и доп. удобства */
    .custom-toast {
        transition: 0.2s;
        pointer-events: none;
        font-family: system-ui;
    }
    .product-card .add-to-cart-btn {
        font-weight: 600;
        transition: background 0.2s, color 0.2s;
    }
    button, .product-card, .cart-info {
        user-select: none;
    }
    @media (max-width: 640px) {
        body {
            padding: 1rem;
        }
        .products-grid {
            gap: 1rem;
        }
    }
</style>
</body>
</html>
