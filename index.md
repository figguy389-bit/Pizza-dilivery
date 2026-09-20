<!DOCTYPE html>  
<html lang="ar" dir="rtl">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>بيتزا دليفري - زاخو | Pizza Delivery</title>  
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet">  
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">  
    <style>  
        :root {  
            --primary: #e63946;  
            --secondary: #1d3557;  
            --accent: #ffb703;  
            --bg: #121212;  
            --card-bg: #1e1e1e;  
            --text: #f8f9fa;  
            --text-muted: #adb5bd;  
            --border: #333;  
        }  
        * {  
            box-sizing: border-box;  
            margin: 0;  
            padding: 0;  
            font-family: 'Cairo', sans-serif;  
        }  
        body {  
            background-color: var(--bg);  
            color: var(--text);  
            min-height: 100vh;  
        }  
        /* Welcome Screen */  
        #welcome-screen {  
            position: fixed;  
            top: 0;  
            left: 0;  
            width: 100%;  
            height: 100%;  
            background: linear-gradient(135deg, #0b0f19, #1a1a2e);  
            display: flex;  
            flex-direction: column;  
            justify-content: center;  
            align-items: center;  
            z-index: 1000;  
            padding: 20px;  
            text-align: center;  
        }  
        .welcome-logo {  
            width: 100px;  
            height: 100px;  
            background: linear-gradient(45deg, var(--primary), var(--accent));  
            border-radius: 25px;  
            display: flex;  
            justify-content: center;  
            align-items: center;  
            font-size: 50px;  
            color: white;  
            margin-bottom: 20px;  
            box-shadow: 0 10px 25px rgba(230,57,70,0.4);  
        }  
        .welcome-title {  
            font-size: 32px;  
            font-weight: 900;  
            margin-bottom: 8px;  
        }  
        .welcome-subtitle {  
            font-size: 16px;  
            color: var(--text-muted);  
            margin-bottom: 30px;  
        }  
        .welcome-card-msg {  
            background: rgba(255, 255, 255, 0.05);  
            border: 1px solid rgba(255, 255, 255, 0.1);  
            padding: 15px 25px;  
            border-radius: 15px;  
            margin-bottom: 30px;  
            max-width: 500px;  
        }  
        .lang-btns {  
            display: flex;  
            flex-direction: column;  
            gap: 12px;  
            width: 100%;  
            max-width: 320px;  
        }  
        .lang-btn {  
            background: var(--card-bg);  
            color: white;  
            border: 1px solid var(--border);  
            padding: 14px;  
            border-radius: 12px;  
            font-size: 18px;  
            font-weight: 700;  
            cursor: pointer;  
            transition: 0.3s;  
        }  
        .lang-btn:hover {  
            background: var(--primary);  
            border-color: var(--primary);  
            transform: translateY(-2px);  
        }  
  
        /* Main App */  
        #app-container {  
            display: none;  
            max-width: 600px;  
            margin: 0 auto;  
            padding-bottom: 100px;  
        }  
        header {  
            background: var(--card-bg);  
            padding: 20px;  
            text-align: center;  
            border-bottom: 1px solid var(--border);  
            position: sticky;  
            top: 0;  
            z-index: 100;  
        }  
        .header-top {  
            display: flex;  
            justify-content: space-between;  
            align-items: center;  
            margin-bottom: 10px;  
        }  
        .admin-trigger {  
            background: transparent;  
            border: 1px solid var(--border);  
            color: var(--text-muted);  
            padding: 6px 12px;  
            border-radius: 8px;  
            font-size: 12px;  
            cursor: pointer;  
        }  
        .restaurant-name {  
            font-size: 24px;  
            font-weight: 900;  
            color: var(--primary);  
        }  
        .banner-msg {  
            background: rgba(255, 183, 3, 0.1);  
            border: 1px solid rgba(255, 183, 3, 0.3);  
            color: var(--accent);  
            padding: 8px;  
            border-radius: 8px;  
            font-size: 14px;  
            margin-top: 8px;  
            font-weight: 600;  
        }  
          
        /* Categories Navigation */  
        .categories-nav {  
            display: flex;  
            gap: 10px;  
            overflow-x: auto;  
            padding: 15px;  
            background: var(--bg);  
            scrollbar-width: none;  
        }  
        .categories-nav::-webkit-scrollbar { display: none; }  
        .cat-btn {  
            background: var(--card-bg);  
            color: var(--text);  
            border: 1px solid var(--border);  
            padding: 8px 16px;  
            border-radius: 20px;  
            white-space: nowrap;  
            font-size: 14px;  
            font-weight: 600;  
            cursor: pointer;  
            transition: 0.2s;  
        }  
        .cat-btn.active {  
            background: var(--primary);  
            border-color: var(--primary);  
        }  
  
        /* Menu Grid */  
        .menu-section {  
            padding: 15px;  
        }  
        .section-title {  
            font-size: 20px;  
            font-weight: 700;  
            margin-bottom: 15px;  
            color: var(--accent);  
            border-bottom: 2px solid var(--border);  
            padding-bottom: 5px;  
        }  
        .items-grid {  
            display: grid;  
            grid-template-columns: repeat(2, 1fr);  
            gap: 15px;  
        }  
        @media (max-width: 400px) {  
            .items-grid { grid-template-columns: 1fr; }  
        }  
        .food-card {  
            background: var(--card-bg);  
            border: 1px solid var(--border);  
            border-radius: 15px;  
            overflow: hidden;  
            display: flex;  
            flex-direction: column;  
            justify-content: space-between;  
            position: relative;  
        }  
        .food-img {  
            width: 100%;  
            height: 130px;  
            object-fit: cover;  
        }  
        .food-details {  
            padding: 12px;  
            flex-grow: 1;  
            display: flex;  
            flex-direction: column;  
            justify-content: space-between;  
        }  
        .food-title {  
            font-size: 15px;  
            font-weight: 700;  
            margin-bottom: 6px;  
        }  
        .food-price {  
            font-size: 14px;  
            font-weight: 600;  
            color: var(--accent);  
            margin-bottom: 10px;  
        }  
        .food-actions {  
            display: flex;  
            gap: 5px;  
        }  
        .add-btn {  
            background: var(--primary);  
            color: white;  
            border: none;  
            padding: 8px;  
            border-radius: 8px;  
            font-size: 13px;  
            font-weight: 600;  
            cursor: pointer;  
            width: 100%;  
            display: flex;  
            justify-content: center;  
            align-items: center;  
            gap: 5px;  
        }  
        .edit-item-btn {  
            background: #333;  
            color: #fff;  
            border: none;  
            padding: 8px;  
            border-radius: 8px;  
            cursor: pointer;  
            display: none;  
        }  
        .admin-mode .edit-item-btn {  
            display: block;  
        }  
  
        /* Cart Floating Bar */  
        .cart-bar {  
            position: fixed;  
            bottom: 20px;  
            left: 20px;  
            right: 20px;  
            max-width: 560px;  
            margin: 0 auto;  
            background: var(--primary);  
            color: white;  
            padding: 15px 20px;  
            border-radius: 15px;  
            display: flex;  
            justify-content: space-between;  
            align-items: center;  
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);  
            cursor: pointer;  
            z-index: 99;  
            transform: translateY(150px);  
            transition: transform 0.3s ease;  
        }  
        .cart-bar.visible {  
            transform: translateY(0);  
        }  
  
        /* Cart Modal */  
        .modal {  
            position: fixed;  
            top: 0;  
            left: 0;  
            width: 100%;  
            height: 100%;  
            background: rgba(0,0,0,0.8);  
            display: none;  
            justify-content: center;  
            align-items: flex-end;  
            z-index: 2000;  
        }  
        .modal.active { display: flex; }  
        .modal-content {  
            background: var(--card-bg);  
            width: 100%;  
            max-width: 600px;  
            max-height: 85vh;  
            border-top-left-radius: 25px;  
            border-top-right-radius: 25px;  
            padding: 20px;  
            overflow-y: auto;  
            border-top: 1px solid var(--border);  
        }  
        .cart-item {  
            display: flex;  
            justify-content: space-between;  
            align-items: center;  
            padding: 10px 0;  
            border-bottom: 1px solid var(--border);  
        }  
        .checkout-btn {  
            background: #25d366;  
            color: white;  
            border: none;  
            width: 100%;  
            padding: 14px;  
            border-radius: 12px;  
            font-size: 16px;  
            font-weight: bold;  
            cursor: pointer;  
            margin-top: 15px;  
            display: flex;  
            justify-content: center;  
            align-items: center;  
            gap: 8px;  
        }  
        .map-link-container {  
            margin-top: 20px;  
            text-align: center;  
        }  
        .map-btn {  
            background: #1d3557;  
            color: white;  
            text-decoration: none;  
            padding: 10px 20px;  
            border-radius: 10px;  
            display: inline-block;  
            font-size: 14px;  
            font-weight: 600;  
        }  
    </style>  
</head>  
<body>  
  
    <!-- Welcome Screen -->  
    <div id="welcome-screen">  
        <div class="welcome-logo">  
            <i class="fa-solid fa-pizza-slice"></i>  
        </div>  
        <div class="welcome-title">بيتزا دليفري</div>  
        <div class="welcome-subtitle">Pizza Delivery - Zakho</div>  
          
        <div class="welcome-card-msg">  
            <div dir="rtl" style="font-weight:700; color: #ffb703; margin-bottom: 5px;">بەخێر هاتن بۆ مینیوی پیتزا دلیڤەری</div>  
            <div dir="rtl" style="font-weight:600; font-size: 14px;">گەهاندن بێ بەرامبەرە بۆ زاخۆ</div>  
        </div>  
  
        <div style="font-size: 14px; color: #adb5bd; margin-bottom: 15px;" dir="rtl">الرجاء اختيار لغتك المفضلة / Please select your language / تكاية زمانێ خو هلبژێره</div>  
          
        <div class="lang-btns">  
            <button class="lang-btn" onclick="selectLang('kur')">کوردی (بادینی)</button>  
            <button class="lang-btn" onclick="selectLang('ar')">العربية</button>  
            <button class="lang-btn" onclick="selectLang('en')">English</button>  
        </div>  
    </div>  
  
    <!-- Main Application -->  
    <div id="app-container">  
        <header>  
            <div class="header-top">  
                <button class="admin-trigger" onclick="openAdminPrompt()">  
                    <i class="fa-solid fa-lock"></i>  
                </button>  
                <div class="restaurant-name" id="ui-store-title">بيتزا دليفري</div>  
                <div style="width: 40px;"></div>  
            </div>  
            <div class="banner-msg" id="ui-banner">گەهاندن بێ بەرامبەرە بۆ زاخۆ - التوصيل مجاني في زاخو</div>  
        </header>  
  
        <!-- Navigation Categories -->  
        <div class="categories-nav" id="cat-nav">  
            <!-- Dynamically populated -->  
        </div>  
  
        <!-- Menu Sections -->  
        <div id="menu-container">  
            <!-- Dynamically populated -->  
        </div>  
  
        <!-- Location Button -->  
        <div class="map-link-container">  
            <a href="https://maps.google.com/?q=37.158360,42.689598" target="_blank" class="map-btn">  
                <i class="fa-solid fa-map-location-dot"></i> موقع المطعم على الخريطة (موقعنا في زاخو)  
            </a>  
        </div>  
    </div>  
  
    <!-- Floating Cart Bar -->  
    <div class="cart-bar" id="cart-bar" onclick="openCartModal()">  
        <div>  
            <i class="fa-solid fa-cart-shopping"></i> <span id="cart-count">0</span> أصناف  
        </div>  
        <div style="font-weight: bold;" id="cart-total">0 د.ع</div>  
    </div>  
  
    <!-- Cart Modal -->  
    <div class="modal" id="cart-modal">  
        <div class="modal-content">  
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">  
                <h3 id="cart-modal-title">سلة الطلبات</h3>  
                <button onclick="closeCartModal()" style="background:none; border:none; color:white; font-size:20px; cursor:pointer;"><i class="fa-solid fa-xmark"></i></button>  
            </div>  
            <div id="cart-items-list"></div>  
            <div style="margin-top: 15px; font-weight: bold; font-size: 18px; display: flex; justify-content: space-between;">  
                <span>المجموع الكلي:</span>  
                <span id="modal-total-price">0 د.ع</span>  
            </div>  
            <div style="margin-top: 15px;">  
                <label style="font-size: 13px; color: var(--text-muted); display: block; margin-bottom: 5px;">رقم الواتساب لإرسال الطلب:</label>  
                <select id="whatsapp-number" style="width: 100%; padding: 10px; background: var(--bg); color: white; border: 1px solid var(--border); border-radius: 8px; margin-bottom: 10px;">  
                    <option value="9647508653005">07508653005</option>  
                    <option value="9647508653007">07508653007</option>  
                </select>  
                <button class="checkout-btn" onclick="sendWhatsAppOrder()">  
                    <i class="fa-brands fa-whatsapp" style="font-size: 20px;"></i> إرسال الطلب عبر الواتساب  
                </button>  
            </div>  
        </div>  
    </div>  
  
    <!-- Edit Item Modal (Admin) -->  
    <div class="modal" id="edit-modal">  
        <div class="modal-content">  
            <h3>تعديل المنتج</h3>  
            <div style="margin-top: 15px;">  
                <label style="font-size: 13px; display: block; margin-bottom: 5px;">اسم المنتج:</label>  
                <input type="text" id="edit-name-input" style="width:100%; padding:10px; background:var(--bg); color:white; border:1px solid var(--border); border-radius:8px; margin-bottom:10px;">  
                  
                <label style="font-size: 13px; display: block; margin-bottom: 5px;">السعر:</label>  
                <input type="text" id="edit-price-input" style="width:100%; padding:10px; background:var(--bg); color:white; border:1px solid var(--border); border-radius:8px; margin-bottom:15px;">  
                  
                <div style="display: flex; gap: 10px;">  
                    <button onclick="saveItemEdit()" style="background:var(--primary); color:white; border:none; padding:10px; border-radius:8px; flex:1; font-weight:bold; cursor:pointer;">حفظ</button>  
                    <button onclick="closeEditModal()" style="background:#333; color:white; border:none; padding:10px; border-radius:8px; flex:1; cursor:pointer;">إلغاء</button>  
                </div>  
            </div>  
        </div>  
    </div>  
  
    <script>  
        // Default Data Structure  
        const defaultMenuData = [  
            {  
                id: "pizza",  
                title: "قسم بيتزا",  
                items: [  
                    { id: "p1", name: "بيتزا ببروني", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1628840042765-356cda07504e?w=500" },  
                    { id: "p2", name: "بيتزا سجق", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500" },  
                    { id: "p3", name: "بيتزا تونا", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=500" },  
                    { id: "p4", name: "بيتزا عادى", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=500" },  
                    { id: "p5", name: "بيتزا ايطالي", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1534308983496-4fabb1a015ee?w=500" },  
                    { id: "p6", name: "بيتزا مريشك", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1565299585323-38d6b0865b47?w=500" },  
                    { id: "p7", name: "بيتزا مارگريتا", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?w=500" },  
                    { id: "p8", name: "لحم بعجين عادى", price: "1000 د.ع", img: "https://images.unsplash.com/photo-1627308595229-7830a5c91f9f?w=500" },  
                    { id: "p9", name: "لحم بعجين دبل", price: "2000 د.ع", img: "https://images.unsplash.com/photo-1627308595229-7830a5c91f9f?w=500" },  
                    { id: "p10", name: "كاده عادي", price: "1500 د.ع", img: "https://images.unsplash.com/photo-1509440159596-0249088772ff?w=500" }  
                ]  
            },  
            {  
                id: "pizza_vip",  
                title: "قسم بيتزا vip",  
                items: [  
                    { id: "v1", name: "بيتزا نوتيلا", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1579751626657-72bc17010498?w=500" },  
                    { id: "v2", name: "بيتزا vip", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500" },  
                    { id: "v3", name: "بيتزا قومبله", price: "100000 د.ع", img: "https://images.unsplash.com/photo-1595751100295-7f90ec1c5b7f?w=500" },  
                    { id: "v4", name: "بيتزا نيف قومبه له", price: "7000 د.ع", img: "https://images.unsplash.com/photo-1541745537411-b8046dc6d66c?w=500" },  
                    { id: "v5", name: "بيتزا عادي", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=500" },  
                    { id: "v6", name: "بيتزا سجق", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500" },  
                    { id: "v7", name: "بيتزا ببروني", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1628840042765-356cda07504e?w=500" },  
                    { id: "v8", name: "بيتزا مارگريتا", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?w=500" },  
                    { id: "v9", name: "بيتزا ايطالي", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1534308983496-4fabb1a015ee?w=500" },  
                    { id: "v10", name: "لحم بعجين", price: "2000 د.ع", img: "https://images.unsplash.com/photo-1627308595229-7830a5c91f9f?w=500" }  
                ]  
            },  
            {  
                id: "grills",  
                title: "قسم المشاوي",  
                items: [  
                    { id: "g1", name: "نفر كباب لحم", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" },  
                    { id: "g2", name: "نصف نفر", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" },  
                    { id: "g3", name: "نفر كباب دجاج", price: "8000 د.ع", img: "https://images.unsplash.com/photo-1603048588665-791ca8aea617?w=500" },  
                    { id: "g4", name: "نفر تكه لحم", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" },  
                    { id: "g5", name: "نفر تكة دجاج", price: "8000 د.ع", img: "https://images.unsplash.com/photo-1603048588665-791ca8aea617?w=500" },  
                    { id: "g6", name: "نفر ميلاك", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" },  
                    { id: "g7", name: "نفر مشكل", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" },  
                    { id: "g8", name: "نفر جەنگ (اجنحه)", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1527477396000-e27163b481c2?w=500" },  
                    { id: "g9", name: "كيلو كباب لحم", price: "25000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" },  
                    { id: "g10", name: "كيلو تكه دجاج", price: "25000 د.ع", img: "https://images.unsplash.com/photo-1603048588665-791ca8aea617?w=500" },  
                    { id: "g11", name: "كيلو تكه لحم", price: "25000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" },  
                    { id: "g12", name: "كيلو مشكل", price: "27000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" },  
                    { id: "g13", name: "منسف مشاوي", price: "30000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" }  
                ]  
            },  
            {  
                id: "wraps",  
                title: "قسم اللفات",  
                items: [  
                    { id: "w1", name: "لفه دجاج عادى", price: "1000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46?w=500" },  
                    { id: "w2", name: "لفه سوري دجاج", price: "2000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46?w=500" },  
                    { id: "w3", name: "لفه فلافل", price: "1000 د.ع", img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e?w=500" },  
                    { id: "w4", name: "ماعون فلافل", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e?w=500" },  
                    { id: "w5", name: "ماعون گص مريشك (دجاج)", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1529692236671-f1f6cf9683ba?w=500" },  
                    { id: "w6", name: "نيڤ ماعون گص مريشك (دجاج)", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1529692236671-f1f6cf9683ba?w=500" },  
                    { id: "w7", name: "لفه لحم (گوشت) عادى", price: "2000 د.ع", img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500" },  
                    { id: "w8", name: "لفه سوري گوشت (لحم)", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500" },  
                    { id: "w9", name: "فلافل سوري", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e?w=500" },  
                    { id: "w10", name: "برگر لحم (گوشت)", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500" },  
                    { id: "w11", name: "برگر مريشك (دجاج)", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46?w=500" },  
                    { id: "w12", name: "دبل چيز برگر", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1586190848861-99aa4a171e90?w=500" },  
                    { id: "w13", name: "دونەر مريشك", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1529692236671-f1f6cf9683ba?w=500" },  
                    { id: "w14", name: "دونەر گوشت", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500" },  
                    { id: "w15", name: "بوكس دجاج", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46?w=500" },  
                    { id: "w16", name: "بوكس لحم", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500" },  
                    { id: "w17", name: "بوكس دايت", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1540420773420-3366772f4999?w=500" },  
                    { id: "w18", name: "دونه ر مشكل جبن", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1529692236671-f1f6cf9683ba?w=500" },  
                    { id: "w19", name: "فنگر", price: "2500 د.ع", img: "https://images.unsplash.com/photo-1573080496219-bb080dd4f877?w=500" },  
                    { id: "w20", name: "وجبة فنگر مع فلافل", price: "6000 د.ع", img: "https://images.unsplash.com/photo-1573080496219-bb080dd4f877?w=500" }  
                ]  
            },  
            {  
                id: "mansaf",  
                title: "قسم المنسف",  
                items: [  
                    { id: "m1", name: "مريشك سادة", price: "8000 د.ع", img: "https://images.unsplash.com/photo-1532550907401-a500c9a57435?w=500" },  
                    { id: "m2", name: "مريشك كامل", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1532550907401-a500c9a57435?w=500" },  
                    { id: "m3", name: "منسف ٢ نفر", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" },  
                    { id: "m4", name: "منسف ٣ نفر", price: "15000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" },  
                    { id: "m5", name: "منسف ٤ نفر", price: "20000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" },  
                    { id: "m6", name: "منسف ٥ نفر", price: "25000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" },  
                    { id: "m7", name: "كبسة سعودي", price: "40000 د.ع", img: "https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=500" }  
                ]  
            },  
            {  
                id: "drinks",  
                title: "قسم المشروبات",  
                items: [  
                    { id: "d1", name: "ببسي", price: "500 د.ع", img: "https://images.unsplash.com/photo-1622483767028-3f66f32aef97?w=500" },  
                    { id: "d2", name: "فانتا برتقال", price: "500 د.ع", img: "https://images.unsplash.com/photo-1624552184280-9e9632bbeee9?w=500" },  
                    { id: "d3", name: "سفن اب", price: "500 د.ع", img: "https://images.unsplash.com/photo-1625772299848-391b6a87d7b3?w=500" },  
                    { id: "d4", name: "چاي كردي", price: "250 د.ع", img: "https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=500" },  
                    { id: "d5", name: "ده و كردي", price: "1000 د.ع", img: "https://images.unsplash.com/photo-1541658016709-82535e94bc69?w=500" }  
                ]  
            }  
        ];  
  
        let menuData = JSON.parse(localStorage.getItem('pizza_menu_data')) || defaultMenuData;  
        let cart = [];  
        let currentEditItem = null;  
  
        function selectLang(lang) {  
            document.getElementById('welcome-screen').style.display = 'none';  
            document.getElementById('app-container').style.display = 'block';  
            renderMenu();  
        }  
  
        function renderMenu() {  
            const nav = document.getElementById('cat-nav');  
            const container = document.getElementById('menu-container');  
            nav.innerHTML = '';  
            container.innerHTML = '';  
  
            menuData.forEach((section, index) => {  
                // Category button  
                const btn = document.createElement('button');  
                btn.className = `cat-btn ${index === 0 ? 'active' : ''}`;  
                btn.innerText = section.title;  
                btn.onclick = () => {  
                    document.querySelectorAll('.cat-btn').forEach(b => b.classList.remove('active'));  
                    btn.classList.add('active');  
                    document.getElementById(section.id).scrollIntoView({ behavior: 'smooth' });  
                };  
                nav.appendChild(btn);  
  
                // Section items  
                const secDiv = document.createElement('div');  
                secDiv.id = section.id;  
                secDiv.className = 'menu-section';  
                secDiv.innerHTML = `<div class="section-title">${section.title}</div>`;  
  
                const grid = document.createElement('div');  
                grid.className = 'items-grid';  
  
                section.items.forEach(item => {  
                    const card = document.createElement('div');  
                    card.className = 'food-card';  
                    card.innerHTML = `  
                        <img src="${item.img}" class="food-img" alt="${item.name}">  
                        <div class="food-details">  
                            <div>  
                                <div class="food-title">${item.name}</div>  
                                <div class="food-price">${item.price}</div>  
                            </div>  
                            <div class="food-actions">  
                                <button class="add-btn" onclick="addToCart('${item.id}', '${item.name}', '${item.price}')">  
                                    <i class="fa-solid fa-plus"></i> اطلب  
                                </button>  
                                <button class="edit-item-btn" onclick="openEditModal('${section.id}', '${item.id}')">  
                                    <i class="fa-solid fa-pen"></i>  
                                </button>  
                            </div>  
                        </div>  
                    `;  
                    grid.appendChild(card);  
                });  
  
                secDiv.appendChild(grid);  
                container.appendChild(secDiv);  
            });  
        }  
  
        function addToCart(id, name, priceStr) {  
            const priceNum = parseInt(priceStr);  
            const existing = cart.find(i => i.id === id);  
            if (existing) {  
                existing.qty++;  
            } else {  
                cart.push({ id, name, price: priceNum, qty: 1 });  
            }  
            updateCartUI();  
        }  
  
        function updateCartUI() {  
            const totalItems = cart.reduce((sum, i) => sum + i.qty, 0);  
            const totalPrice = cart.reduce((sum, i) => sum + (i.price * i.qty), 0);  
              
            document.getElementById('cart-count').innerText = totalItems;  
            document.getElementById('cart-total').innerText = totalPrice + ' د.ع';  
  
            const cartBar = document.getElementById('cart-bar');  
            if (totalItems > 0) {  
                cartBar.classList.add('visible');  
            } else {  
                cartBar.classList.remove('visible');  
            }  
        }  
  
        function openCartModal() {  
            const list = document.getElementById('cart-items-list');  
            list.innerHTML = '';  
            let totalPrice = 0;  
  
            cart.forEach(item => {  
                totalPrice += item.price * item.qty;  
                const div = document.createElement('div');  
                div.className = 'cart-item';  
                div.innerHTML = `  
                    <div>  
                        <div style="font-weight:700;">${item.name}</div>  
                        <div style="font-size:13px; color:var(--text-muted);">${item.price * item.qty} د.ع (${item.qty}x)</div>  
                    </div>  
                    <div style="display:flex; gap:8px; align-items:center;">  
                        <button onclick="changeQty('${item.id}', 1)" style="background:#333; color:white; border:none; width:25px; height:25px; border-radius:5px; cursor:pointer;">+</button>  
                        <span>${item.qty}</span>  
                        <button onclick="changeQty('${item.id}', -1)" style="background:#333; color:white; border:none; width:25px; height:25px; border-radius:5px; cursor:pointer;">-</button>  
                    </div>  
                `;  
                list.appendChild(div);  
            });  
  
            document.getElementById('modal-total-price').innerText = totalPrice + ' د.ع';  
            document.getElementById('cart-modal').classList.add('active');  
        }  
  
        function closeCartModal() {  
            document.getElementById('cart-modal').classList.remove('active');  
        }  
  
        function changeQty(id, delta) {  
            const item = cart.find(i => i.id === id);  
            if (item) {  
                item.qty += delta;  
                if (item.qty <= 0) {  
                    cart = cart.filter(i => i.id !== id);  
                }  
            }  
            updateCartUI();  
            openCartModal();  
        }  
  
        function sendWhatsAppOrder() {  
            if (cart.length === 0) return;  
            const phone = document.getElementById('whatsapp-number').value;  
            let message = "مرحباً، أود طلب الأطمة التالية من بيتزا دليفري (زاخو):\n\n";  
            let total = 0;  
            cart.forEach(i => {  
                message += `- ${i.name} (${i.qty}x) : ${i.price * i.qty} د.ع\n`;  
                total += i.price * i.qty;  
            });  
            message += `\nالمجموع الكلي: ${total} د.ع\nرابط الموقع: https://maps.google.com/?q=37.158360,42.689598`;  
  
            const url = `https://wa.me/${phone}?text=${encodeURIComponent(message)}`;  
            window.open(url, '_blank');  
        }  
  
        // Admin Security & Editing  
        function openAdminPrompt() {  
            const code = prompt("ادخل الرمز للاكمال");  
            if (code === "30067") {  
                document.body.classList.toggle('admin-mode');  
                alert("تم تفعيل وضع التعديل بنجاح!");  
            } else if (code !== null) {  
                alert("الرمز غير صحيح!");  
            }  
        }  
  
        function openEditModal(secId, itemId) {  
            const sec = menuData.find(s => s.id === secId);  
            const item = sec.items.find(i => i.id === itemId);  
            currentEditItem = { secId, itemId };  
  
            document.getElementById('edit-name-input').value = item.name;  
            document.getElementById('edit-price-input').value = item.price;  
            document.getElementById('edit-modal').classList.add('active');  
        }  
  
        function closeEditModal() {  
            document.getElementById('edit-modal').classList.remove('active');  
            currentEditItem = null;  
        }  
  
        function saveItemEdit() {  
            if (!currentEditItem) return;  
            const newName = document.getElementById('edit-name-input').value;  
            const newPrice = document.getElementById('edit-price-input').value;  
  
            const sec = menuData.find(s => s.id === currentEditItem.secId);  
            const item = sec.items.find(i => i.id === currentEditItem.itemId);  
  
            item.name = newName;  
            item.price = newPrice;  
  
            localStorage.setItem('pizza_menu_data', JSON.stringify(menuData));  
            closeEditModal();  
            renderMenu();  
            alert("تم حفظ التعديل بنجاح وسيظل محفوظاً!");  
        }  
    </script>  
</body>  
</html>  
