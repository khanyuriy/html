<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Мобильное приложение - Верстка</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        :root {
            --primary-red: #E60023; /* Примерный красный цвет */
            --primary-orange: #FF5722; /* Примерный оранжевый цвет */
            --light-grey: #F5F5F5;
            --medium-grey: #E0E0E0;
            --dark-grey: #333;
            --text-color: #212121;
            --placeholder-color: #9E9E9E;
            --border-radius-base: 12px;
            --padding-base: 16px;
            --margin-base: 16px;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--light-grey);
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        .container {
            flex-grow: 1;
            padding-bottom: 70px; /* Отступ для нижнего навигационного бара */
        }

        /* --- 1. Верхний бар (Хедер) --- */
        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px var(--padding-base);
            background-color: #fff;
            color: var(--text-color);
            font-size: 14px;
            font-weight: 500;
        }

        .header-top-right i {
            margin-left: 6px;
        }

        /* --- 2. Поисковый и навигационный бар --- */
        .header-main {
            background-color: #fff;
            padding: 10px var(--padding-base);
            padding-bottom: 0; /* Отступ вниз уберем, чтобы элементы прилипли */
        }

        .header-location-rewards {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }

        .location {
            display: flex;
            align-items: center;
            font-size: 15px;
            font-weight: 500;
            color: var(--text-color);
        }

        .location i {
            margin-left: 5px;
            font-size: 10px;
            color: var(--placeholder-color);
        }

        .rewards {
            display: flex;
            align-items: center;
            background-color: var(--primary-orange);
            color: #fff;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
        }

        .rewards i {
            margin-left: 5px;
            font-size: 16px;
        }

        .search-bar {
            display: flex;
            align-items: center;
            gap: 8px;
            padding-bottom: 10px;
        }

        .search-icon-wrapper {
            width: 38px;
            height: 38px;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: var(--medium-grey); /* Фон для иконки гамбургера */
            border-radius: 50%;
            cursor: pointer;
        }
        .search-icon-wrapper i {
            color: var(--text-color);
            font-size: 18px;
        }

        .search-input-container {
            flex-grow: 1;
            display: flex;
            align-items: center;
            background-color: var(--light-grey);
            border-radius: var(--border-radius-base);
            padding: 8px 12px;
        }

        .search-input-container i {
            color: var(--placeholder-color);
            margin-right: 8px;
        }

        .search-input-container input {
            border: none;
            background: none;
            outline: none;
            flex-grow: 1;
            font-size: 16px;
            color: var(--text-color);
            padding: 0;
        }

        .search-input-container input::placeholder {
            color: var(--placeholder-color);
        }

        .camera-icon-wrapper {
            width: 38px;
            height: 38px;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: var(--light-grey); /* Фон для иконки камеры */
            border-radius: 50%;
            cursor: pointer;
        }
        .camera-icon-wrapper i {
            color: var(--text-color);
            font-size: 18px;
        }

        /* --- 3. Горизонтальное меню категорий/фильтров --- */
        .category-nav {
            background-color: #fff;
            padding: 10px 0;
            overflow-x: auto;
            white-space: nowrap;
            -webkit-overflow-scrolling: touch; /* Для плавного скролла на iOS */
        }

        .category-nav::-webkit-scrollbar {
            display: none; /* Скрыть скроллбар для Webkit-браузеров */
        }

        .category-nav-inner {
            display: flex;
            padding: 0 var(--padding-base);
            gap: 24px; /* Отступ между элементами */
        }

        .category-item {
            display: inline-block; /* Для корректного скролла */
            font-size: 17px;
            font-weight: 500;
            color: var(--placeholder-color);
            padding-bottom: 8px;
            position: relative;
            cursor: pointer;
            transition: color 0.2s ease;
        }

        .category-item.active {
            color: var(--primary-red);
            font-weight: 600;
        }

        .category-item.active::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 80%; /* Длина подчеркивания */
            height: 3px;
            background-color: var(--primary-red);
            border-radius: 2px;
        }

        /* --- 4. Рекламный баннер/акция --- */
        .promo-banner {
            background-color: var(--primary-red);
            margin: var(--margin-base);
            border-radius: var(--border-radius-base);
            padding: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            overflow: hidden;
            position: relative;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        .promo-banner img {
            height: 70px; /* Высота изображения */
            width: auto;
            position: absolute;
            left: -15px; /* Выступает за левый край */
            bottom: 0;
        }

        .promo-content {
            margin-left: 70px; /* Отступ для изображения */
            color: #fff;
            flex-grow: 1;
        }

        .promo-content .title {
            font-size: 19px;
            font-weight: 700;
            margin-bottom: 2px;
            line-height: 1.2;
        }

        .promo-content .old-price {
            text-decoration: line-through;
            font-size: 13px;
            color: rgba(255, 255, 255, 0.7);
            margin-left: 5px;
        }

        .promo-content .subtitle {
            font-size: 12px;
            color: rgba(255, 255, 255, 0.9);
        }

        .promo-arrow {
            color: #fff;
            font-size: 20px;
        }

        /* --- 5. Основной контент --- */
        .main-content {
            padding: 0 var(--padding-base);
            padding-top: var(--margin-base);
        }

        .huawei-banner {
            background-color: #000;
            color: #fff;
            border-radius: var(--border-radius-base);
            padding: var(--padding-base);
            padding-bottom: 0;
            position: relative;
            overflow: hidden;
            height: 220px; /* Фиксированная высота баннера */
            margin-bottom: var(--margin-base);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        .huawei-banner-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 10px;
            position: relative; /* Чтобы текст был выше изображений */
            z-index: 2;
        }

        .huawei-banner-header .title {
            font-size: 19px;
            font-weight: 700;
            line-height: 1.2;
        }

        .huawei-banner-header .ad-tag {
            background-color: rgba(255, 255, 255, 0.2);
            font-size: 10px;
            padding: 4px 8px;
            border-radius: 4px;
            text-transform: uppercase;
            font-weight: 600;
        }

        .huawei-phones {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            display: flex;
            justify-content: center;
            align-items: flex-end;
            height: calc(100% - 60px); /* Высота области телефонов */
            z-index: 1;
        }

        .huawei-phone {
            width: 140px; /* Ширина телефона */
            height: 200px; /* Высота телефона */
            object-fit: contain;
            position: absolute;
            bottom: -20px; /* Немного ниже края, чтобы создать эффект погружения */
        }
        .huawei-phone.phone-1 {
            left: 10%;
            transform: translateX(-50%) rotate(-5deg);
            z-index: 0;
        }
        .huawei-phone.phone-2 {
            z-index: 2; /* Центральный телефон выше */
            transform: translateY(-10px);
        }
        .huawei-phone.phone-3 {
            right: 10%;
            transform: translateX(50%) rotate(5deg);
            z-index: 0;
        }


        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: var(--margin-base);
        }

        .product-card {
            background-color: #fff;
            border-radius: var(--border-radius-base);
            overflow: hidden;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
            display: flex;
            flex-direction: column;
            position: relative;
        }

        .product-card-image {
            width: 100%;
            height: 180px; /* Фиксированная высота для изображений */
            object-fit: cover;
            display: block;
            border-radius: var(--border-radius-base) var(--border-radius-base) 0 0;
        }

        .product-card .favorite-icon {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 50%;
            width: 30px;
            height: 30px;
            display: flex;
            justify-content: center;
            align-items: center;
            color: var(--placeholder-color);
            font-size: 14px;
            cursor: pointer;
        }

        .product-card-info {
            padding: 12px;
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .product-card-info .title {
            font-size: 15px;
            font-weight: 500;
            color: var(--text-color);
            line-height: 1.3;
            max-height: 3.9em; /* Примерно 3 строки */
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: normal;
        }

        .product-card.card-featured .product-card-image {
            height: 220px; /* Чуть выше, чем обычная карточка */
        }
        .product-card.card-featured .product-card-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .product-card.card-featured .overlay-text {
            position: absolute;
            top: 15px;
            left: 15px;
            color: #fff;
            text-shadow: 0 1px 3px rgba(0,0,0,0.5);
            line-height: 1;
            z-index: 1;
        }

        .product-card.card-featured .overlay-text .main-title {
            font-size: 28px;
            font-weight: 800;
            color: var(--primary-red);
            margin-bottom: 5px;
        }

        .product-card.card-featured .overlay-text .subtitle {
            font-size: 14px;
            font-weight: 500;
            color: #fff;
        }


        /* --- 6. Нижний навигационный бар (Футер) --- */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background-color: #fff;
            display: flex;
            justify-content: space-around;
            align-items: center;
            height: 60px;
            border-top: 1px solid var(--medium-grey);
            box-shadow: 0 -2px 5px rgba(0,0,0,0.05);
            z-index: 1000;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            font-size: 10px;
            color: var(--placeholder-color);
            cursor: pointer;
        }

        .nav-item i {
            font-size: 22px;
            margin-bottom: 4px;
            color: inherit; /* Иконка наследует цвет родителя */
        }

        .nav-item.active {
            color: var(--primary-red);
        }
    </style>
</head>
<body>

    <div class="header-top">
        <div class="header-top-left">09:36</div>
        <div class="header-top-right">
            <i class="fas fa-wifi"></i>
            <i class="fas fa-signal"></i>
            <i class="fas fa-battery-full"></i> 94
        </div>
    </div>

    <div class="header-main">
        <div class="header-location-rewards">
            <div class="location">
                Вешняковская улица, 22к2
                <i class="fas fa-chevron-right"></i>
            </div>
            <div class="rewards">
                285 <i class="fas fa-coins"></i>
            </div>
        </div>
        <div class="search-bar">
            <div class="search-icon-wrapper">
                <i class="fas fa-bars"></i>
            </div>
            <div class="search-input-container">
                <i class="fas fa-search"></i>
                <input type="text" placeholder="Найти товары">
            </div>
            <div class="camera-icon-wrapper">
                <i class="fas fa-camera"></i>
            </div>
        </div>
    </div>

    <div class="category-nav" id="categoryNav">
        <div class="category-nav-inner">
            <div class="category-item active">Для вас</div>
            <div class="category-item">Ниже рынка</div>
            <div class="category-item">Ultima</div>
            <div class="category-item">Одежда</div>
            <div class="category-item">Электроника</div>
            <div class="category-item">Дом и сад</div>
            <div class="category-item">Красота</div>
        </div>
    </div>

    <div class="promo-banner">
        <img src="https://via.placeholder.com/100x100?text=Массажер" alt="Массажер">
        <div class="promo-content">
            <div class="title">Массажер за 2 999 ₽ <span class="old-price">4 820 ₽</span></div>
            <div class="subtitle">Распродажа с 28 июля</div>
        </div>
        <i class="fas fa-chevron-right promo-arrow"></i>
    </div>

    <div class="main-content">
        <div class="huawei-banner">
            <div class="huawei-banner-header">
                <div class="title">Серия HUAWEI Pura 70</div>
                <div class="ad-tag">Реклама</div>
            </div>
            <div class="huawei-phones">
                <img src="https://via.placeholder.com/150x250/333333/FFFFFF?text=Phone+1" alt="Телефон 1" class="huawei-phone phone-1">
                <img src="https://via.placeholder.com/150x250/C2006B/FFFFFF?text=Phone+2" alt="Телефон 2" class="huawei-phone phone-2">
                <img src="https://via.placeholder.com/150x250/F5F5F5/333333?text=Phone+3" alt="Телефон 3" class="huawei-phone phone-3">
            </div>
        </div>

        <div class="product-grid">
            <div class="product-card">
                <img src="https://via.placeholder.com/200x180?text=Матрас" alt="Надувной матрас" class="product-card-image">
                <div class="favorite-icon"><i class="far fa-heart"></i></div>
                <div class="product-card-info">
                    <div class="title">Надувной матрас в машину, кровать н...</div>
                </div>
            </div>

            <div class="product-card card-featured">
                <img src="https://via.placeholder.com/200x220?text=Девушка" alt="Заглушки" class="product-card-image">
                <div class="favorite-icon"><i class="far fa-heart"></i></div>
                <div class="overlay-text">
                    <div class="main-title">ЗАГЛУШКИ</div>
                    <div class="subtitle">МЕЖДУ СИДЕНЬЯМИ</div>
                </div>
                <div class="product-card-info">
                    <div class="title">Вставка заглушка между сиденьями ...</div>
                </div>
            </div>
        </div>
    </div>

    <div class="bottom-nav">
        <div class="nav-item active">
            <i class="fas fa-home"></i>
            </div>
        <div class="nav-item">
            <i class="fas fa-list-alt"></i>
            </div>
        <div class="nav-item">
            <i class="fas fa-shopping-basket"></i>
            </div>
        <div class="nav-item">
            <i class="far fa-heart"></i>
            </div>
        <div class="nav-item">
            <i class="fas fa-user"></i>
            </div>
    </div>

    <script>
        // JavaScript для горизонтального скролла категорий (если требуется)
        document.addEventListener('DOMContentLoaded', () => {
            const categoryNav = document.getElementById('categoryNav');
            const activeCategory = categoryNav.querySelector('.category-item.active');

            if (activeCategory) {
                // Прокрутить до активного элемента при загрузке
                categoryNav.scrollLeft = activeCategory.offsetLeft - (categoryNav.offsetWidth / 2) + (activeCategory.offsetWidth / 2);
            }

            // Добавление интерактивности для категорий (опционально)
            const categoryItems = categoryNav.querySelectorAll('.category-item');
            categoryItems.forEach(item => {
                item.addEventListener('click', () => {
                    categoryItems.forEach(i => i.classList.remove('active'));
                    item.classList.add('active');
                    // Прокрутка к выбранному элементу
                    categoryNav.scrollLeft = item.offsetLeft - (categoryNav.offsetWidth / 2) + (item.offsetWidth / 2);
                });
            });
        });
    </script>
</body>
</html>
