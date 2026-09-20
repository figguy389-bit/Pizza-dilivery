<!DOCTYPE html>  
<html lang="ar" dir="rtl">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>بيتزا دليفري - Zakho Pizza Delivery</title>  
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;900&display=swap" rel="stylesheet">  
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">  
    <style>  
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Tajawal', sans-serif; }  
        body { background: #121212; color: #fff; min-height: 100vh; }  
        .screen { display: none; }  
        .screen.active { display: block; }  
          
        /* Welcome Screen */  
        #welcome-screen {  
            background: linear-gradient(135deg, #1a0505 0%, #000 100%);  
            min-height: 100vh;  
            display: flex;  
            flex-direction: column;  
            align-items: center;  
            justify-content: center;  
            padding: 20px;  
            text-align: center;  
        }  
        .welcome-logo { width: 120px; height: 120px; border-radius: 20px; object-fit: cover; margin-bottom: 20px; border: 3px solid #ff4757; box-shadow: 0 10px 30px rgba(255,71,87,0.3); }  
        .welcome-title { font-size: 28px; font-weight: 900; margin-bottom: 10px; color: #fff; }  
        .welcome-sub { font-size: 16px; color: #aaa; margin-bottom: 30px; }  
        .lang-card { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 15px; padding: 20px; width: 100%; max-width: 400px; margin-bottom: 20px; }  
        .lang-text { font-size: 16px; line-height: 1.6; color: #f1f1f1; margin-bottom: 15px; font-weight: 700; }  
        .lang-btns { display: flex; gap: 10px; justify-content: center; }  
        .btn-lang { background: #ff4757; color: white; border: none; padding: 10px 20px; border-radius: 8px; font-weight: 700; cursor: pointer; transition: 0.2s; }  
        .btn-lang:hover { background: #ff6b81; }  
  
        /* Main App Header */  
        .app-header { background: #1e1e1e; padding: 15px 20px; display: flex; align-items: center; justify-content: space-between; border-bottom: 1px solid #333; position: sticky; top: 0; z-index: 100; }  
        .header-logo-area { display: flex; align-items: center; gap: 12px; }  
        .header-logo { width: 45px; height: 45px; border-radius: 50%; object-fit: cover; border: 2px solid #ff4757; }  
        .header-title h1 { font-size: 18px; font-weight: 700; }  
        .header-title p { font-size: 12px; color: #aaa; }  
        .header-actions { display: flex; gap: 10px; }  
        .icon-btn { background: #2c2c2c; border: none; color: white; width: 40px; height: 40px; border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; font-size: 16px; }  
  
        /* Categories Bar */  
        .categories-container { display: flex; overflow-x: auto; padding: 15px; gap: 10px; background: #181818; border-bottom: 1px solid #282828; scrollbar-width: none; }  
        .categories-container::-webkit-scrollbar { display: none; }  
        .cat-chip { background: #262626; border: 1px solid #383838; padding: 8px 16px; border-radius: 20px; white-space: nowrap; font-size: 14px; cursor: pointer; color: #ccc; transition: 0.2s; }  
        .cat-chip.active { background: #ff4757; color: white; border-color: #ff4757; font-weight: 700; }  
  
        /* Products Grid */  
        .products-section { padding: 15px; max-width: 1200px; margin: 0 auto; }  
        .section-title { font-size: 20px; font-weight: 700; margin-bottom: 15px; color: #ff4757; border-right: 4px solid #ff4757; padding-right: 10px; }  
        .products-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 15px; margin-bottom: 30px; }  
        .product-card { background: #1c1c1c; border-radius: 12px; overflow: hidden; border: 1px solid #2c2c2c; display: flex; flex-direction: column; position: relative; }  
        .product-img-wrap { width: 100%; height: 160px; background: #252525; position: relative; overflow: hidden; }  
        .product-img { width: 100%; height: 100%; object-fit: cover; }  
        .product-info { padding: 15px; display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between; }  
        .product-name { font-size: 16px; font-weight: 700; margin-bottom: 8px; }  
        .product-price { font-size: 15px; color: #ff4757; font-weight: 700; margin-bottom: 12px; }  
        .product-actions { display: flex; gap: 8px; }  
        .btn-add { background: #ff4757; color: white; border: none; padding: 8px 12px; border-radius: 8px; font-weight: 700; flex-grow: 1; cursor: pointer; font-size: 14px; }  
        .btn-edit-item { background: #333; color: #fff; border: none; padding: 8px 12px; border-radius: 8px; cursor: pointer; }  
  
        /* Cart Floating Bar */  
        .cart-float { position: fixed; bottom: 20px; left: 20px; right: 20px; background: #ff4757; color: white; padding: 15px 20px; border-radius: 14px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 10px 25px rgba(255,71,87,0.4); z-index: 99; cursor: pointer; display: none; max-width: 600px; margin: 0 auto; }  
  
        /* Modals */  
        .modal { position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.8); z-index: 1000; display: none; align-items: center; justify-content: center; padding: 20px; }  
        .modal-content { background: #1e1e1e; border-radius: 15px; width: 100%; max-width: 500px; padding: 20px; border: 1px solid #333; max-height: 90vh; overflow-y: auto; }  
        .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; }  
        .modal-title { font-size: 18px; font-weight: 700; }  
        .close-modal { background: none; border: none; color: #aaa; font-size: 20px; cursor: pointer; }  
        .form-group { margin-bottom: 15px; }  
        .form-label { display: block; font-size: 13px; color: #aaa; margin-bottom: 5px; }  
        .form-input { width: 100%; background: #2a2a2a; border: 1px solid #3a3a3a; padding: 10px; border-radius: 8px; color: white; font-size: 14px; }  
        .btn-save { background: #2ed573; color: white; border: none; width: 100%; padding: 12px; border-radius: 8px; font-weight: 700; cursor: pointer; margin-top: 10px; }  
  
        .admin-badge { position: fixed; top: 75px; right: 20px; background: #ff4757; color: white; padding: 5px 12px; border-radius: 20px; font-size: 12px; font-weight: 700; z-index: 98; display: none; box-shadow: 0 4px 10px rgba(0,0,0,0.3); }  
    </style>  
</head>  
<body>  
  
    <!-- Welcome Screen -->  
    <div id="welcome-screen" class="screen active">  
        <img id="welcome-logo-img" src="https://images.unsplash.com/photo-1513104890138-7c749659a591" class="welcome-logo" alt="Logo">  
        <h1 class="welcome-title" id="w-title">بيتزا دليفري</h1>  
        <p class="welcome-sub">Zakho Pizza Delivery & Restaurant</p>  
          
        <div class="lang-card">  
            <div class="lang-text">کوردی (بادینی)<br>بخير هاتي بو منيو بيتزا دليڤەري<br>گەهاندن بێ بەرامبەرە بو زاخو</div>  
            <div class="lang-btns">  
                <button class="btn-lang" onclick="setLanguage('ku')">کوردی</button>  
            </div>  
        </div>  
  
        <div class="lang-card">  
            <div class="lang-text">العربية<br>أهلاً بك في منيو بيتزا دليفري<br>التوصيل مجاني إلى زاخو</div>  
            <div class="lang-btns">  
                <button class="btn-lang" onclick="setLanguage('ar')">عربي</button>  
            </div>  
        </div>  
  
        <div class="lang-card">  
            <div class="lang-text">English<br>Welcome to Pizza Delivery Menu<br>Free delivery to Zakho</div>  
            <div class="lang-btns">  
                <button class="btn-lang" onclick="setLanguage('en')">English</button>  
            </div>  
        </div>  
    </div>  
  
    <!-- Main Menu Screen -->  
    <div id="main-screen" class="screen">  
        <div class="admin-badge" id="admin-badge-indicator"><i class="fa-solid fa-lock-open"></i> وضع التعديل مَفعل</div>  
          
        <header class="app-header">  
            <div class="header-logo-area">  
                <img id="header-logo-img" src="https://images.unsplash.com/photo-1513104890138-7c749659a591" class="header-logo" alt="Logo">  
                <div class="header-title">  
                    <h1 id="h-main-title">بيتزا دليفري</h1>  
                    <p>zakho - زاخو</p>  
                </div>  
            </div>  
            <div class="header-actions">  
                <button class="icon-btn" onclick="openAdminModal()" title="التعديل"><i class="fa-solid fa-gear"></i></button>  
                <button class="icon-btn" onclick="openLocation()" title="الموقع"><i class="fa-solid fa-location-dot"></i></button>  
            </div>  
        </header>  
  
        <div class="categories-container" id="categories-bar">  
            <!-- Categories injected dynamically -->  
        </div>  
  
        <main class="products-section" id="menu-container">  
            <!-- Products injected dynamically -->  
        </main>  
  
        <div class="cart-float" id="cart-float" onclick="openCartModal()">  
            <div><i class="fa-solid fa-cart-shopping"></i> <span id="cart-count">0</span> منتجات</div>  
            <div><span id="cart-total">0</span> د.ع <i class="fa-solid fa-arrow-left"></i></div>  
        </div>  
    </div>  
  
    <!-- Admin PIN Modal -->  
    <div class="modal" id="admin-modal">  
        <div class="modal-content">  
            <div class="modal-header">  
                <h3 class="modal-title">لوحة التحكم</h3>  
                <button class="close-modal" onclick="closeModal('admin-modal')">&times;</button>  
            </div>  
            <div class="form-group" id="pin-section">  
                <label class="form-label">ادخل الرمز للاكمال</label>  
                <input type="password" id="admin-pin-input" class="form-input" placeholder="•••••">  
                <button class="btn-save" onclick="verifyAdminPin()">دخول</button>  
            </div>  
            <div id="admin-controls" style="display:none;">  
                <p style="color: #2ed573; margin-bottom: 15px; font-weight: 700;">تم تفعيل وضع التعديل بنجاح!</p>  
                <button class="btn-save" style="background:#ff4757; margin-bottom: 10px;" onclick="addNewProductModal()">+ إضافة منتج جديد</button>  
                <button class="btn-save" style="background:#3742fa;" onclick="changeLogoPrompt()">تغيير اللوجو الرئيسي</button>  
            </div>  
        </div>  
    </div>  
  
    <!-- Item Edit Modal -->  
    <div class="modal" id="edit-item-modal">  
        <div class="modal-content">  
            <div class="modal-header">  
                <h3 class="modal-title">تعديل المنتج</h3>  
                <button class="close-modal" onclick="closeModal('edit-item-modal')">&times;</button>  
            </div>  
            <input type="hidden" id="edit-item-id">  
            <div class="form-group">  
                <label class="form-label">اسم المنتج</label>  
                <input type="text" id="edit-item-name" class="form-input">  
            </div>  
            <div class="form-group">  
                <label class="form-label">السعر (د.ع)</label>  
                <input type="text" id="edit-item-price" class="form-input">  
            </div>  
            <div class="form-group">  
                <label class="form-label">صورة المنتج (من الاستوديو)</label>  
                <input type="file" id="edit-item-file" class="form-input" accept="image/*">  
            </div>  
            <button class="btn-save" onclick="saveItemChanges()">حفظ التعديلات</button>  
        </div>  
    </div>  
  
    <!-- Cart Modal -->  
    <div class="modal" id="cart-modal">  
        <div class="modal-content">  
            <div class="modal-header">  
                <h3 class="modal-title">سلة الطلبات</h3>  
                <button class="close-modal" onclick="closeModal('cart-modal')">&times;</button>  
            </div>  
            <div id="cart-items-list" style="margin-bottom: 15px; max-height: 200px; overflow-y: auto;"></div>  
            <div class="form-group">  
                <label class="form-label">رقم الهاتف / العنوان</label>  
                <input type="text" id="customer-address" class="form-input" placeholder="اكتب عنوانك ورقم هاتفك هنا...">  
            </div>  
            <label class="form-label">اختر رقم الواتساب للطلب:</label>  
            <div style="display: flex; gap: 10px; margin-top: 10px;">  
                <button class="btn-save" style="background:#25d366; margin-top:0;" onclick="sendWhatsApp('07508653006')">واتساب 1 (07508653006)</button>  
                <button class="btn-save" style="background:#25d366; margin-top:0;" onclick="sendWhatsApp('07508653007')">واتساب 2 (07508653007)</button>  
            </div>  
        </div>  
    </div>  
  
    <script>  
        const defaultData = {  
            logo: "https://images.unsplash.com/photo-1513104890138-7c749659a591",  
            categories: [  
                {  
                    id: "pizza",  
                    name: "بيتزا",  
                    items: [  
                        { id: 1, name: "بيتزا ببروني", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1628840042765-356cda07504e" },  
                        { id: 2, name: "بيتزا سجق", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1513104890138-7c749659a591" },  
                        { id: 3, name: "بيتزا تونا", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38" },  
                        { id: 4, name: "بيتزا عادى", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002" },  
                        { id: 5, name: "بيتزا ايطالي", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1534308983496-4fabb1a015ee" },  
                        { id: 6, name: "بيتزا مريشك", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1565299585323-38d6b0865b47" },  
                        { id: 7, name: "بيتزا مارگريتا", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1604382355076-af4b0eb60143" },  
                        { id: 8, name: "لحم بعجين عادى", price: "1000 د.ع", img: "https://images.unsplash.com/photo-1627308595229-7830a5c91f9f" },  
                        { id: 9, name: "لحم بعجين دبل", price: "2000 د.ع", img: "https://images.unsplash.com/photo-1627308595229-7830a5c91f9f" },  
                        { id: 10, name: "كاده عادي", price: "1500 د.ع", img: "https://images.unsplash.com/photo-1541544741938-0af808871cc0" }  
                    ]  
                },  
                {  
                    id: "pizza-vip",  
                    name: "بيتزا VIP",  
                    items: [  
                        { id: 11, name: "بيتزا نوتيلا", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1579714544004-94285e683713" },  
                        { id: 12, name: "بيتزا vip", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1513104890138-7c749659a591" },  
                        { id: 13, name: "بيتزا قومبله", price: "15000 د.ع", img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e" },  
                        { id: 14, name: "بيتزا نيف قومبه له", price: "7000 د.ع", img: "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38" },  
                        { id: 15, name: "بيتزا عادي", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002" },  
                        { id: 16, name: "بيتزا سجق", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1513104890138-7c749659a591" },  
                        { id: 17, name: "بيتزا ببروني", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1628840042765-356cda07504e" },  
                        { id: 18, name: "بيتزا مارگريتا", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1604382355076-af4b0eb60143" },  
                        { id: 19, name: "بيتزا ايطالي", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1534308983496-4fabb1a015ee" },  
                        { id: 20, name: "لحم بعجين", price: "2000 د.ع", img: "https://images.unsplash.com/photo-1627308595229-7830a5c91f9f" }  
                    ]  
                },  
                {  
                    id: "grills",  
                    name: "المشاوي",  
                    items: [  
                        { id: 21, name: "نفر كباب لحم", price: "10 الاف", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1" },  
                        { id: 22, name: "نصف نفر", price: "5 الاف", img: "https://images.unsplash.com/photo-1529193591184-b1d58069ecdd" },  
                        { id: 23, name: "نفر كباب دجاج", price: "8000 د.ع", img: "https://images.unsplash.com/photo-1603048588665-791ca8aea617" },  
                        { id: 24, name: "نفر تكه لحم", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947" },  
                        { id: 25, name: "نفر تكة دجاج", price: "8000 د.ع", img: "https://images.unsplash.com/photo-1532550907401-a500c9a57435" },  
                        { id: 26, name: "نفر ميلاك", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1" },  
                        { id: 27, name: "نفر مشكل", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947" },  
                        { id: 28, name: "نفر جەنگ (اجنحه)", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445" },  
                        { id: 29, name: "كيلو كباب لحم", price: "25 الف", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1" },  
                        { id: 30, name: "كيلو تكه دجاج", price: "25 الف", img: "https://images.unsplash.com/photo-1532550907401-a500c9a57435" },  
                        { id: 31, name: "كيلو تكه لحم", price: "25 الف", img: "https://images.unsplash.com/photo-1544025162-d76694265947" },  
                        { id: 32, name: "كيلو مشكل", price: "27 الف", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1" },  
                        { id: 33, name: "منسف مشاوي", price: "30 الف", img: "https://images.unsplash.com/photo-1544025162-d76694265947" }  
                    ]  
                },  
                {  
                    id: "sandwiches",  
                    name: "اللفات",  
                    items: [  
                        { id: 34, name: "لفه دجاج عادى", price: "1000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46" },  
                        { id: 35, name: "لفه سوري دجاج", price: "2000 د.ع", img: "https://images.unsplash.com/photo-1528735602780-2552fd46c7af" },  
                        { id: 36, name: "لفه فلافل", price: "1000 د.ع", img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e" },  
                        { id: 37, name: "ماعون فلافل", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e" },  
                        { id: 38, name: "ماعون گص مريشك (دجاج)", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46" },  
                        { id: 39, name: "نيڤ ماعون گص مريشك (دجاج)", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46" },  
                        { id: 40, name: "لفه لحم (گوشت) عادى", price: "2000 د.ع", img: "https://images.unsplash.com/photo-1550547660-d9450f859349" },  
                        { id: 41, name: "لفه سوري گوشت (لحم)", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1550547660-d9450f859349" },  
                        { id: 42, name: "فلافل سوري", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e" },  
                        { id: 43, name: "برگر لحم (گوشت)", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd" },  
                        { id: 44, name: "برگر مريشك (دجاج)", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1625813506062-0aeb1d7a094b" },  
                        { id: 45, name: "دبل چيز برگر", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1586190848861-99aa4a171e90" },  
                        { id: 46, name: "دونەر مريشك", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46" },  
                        { id: 47, name: "دونەر گوشت", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1550547660-d9450f859349" },  
                        { id: 48, name: "بوكس دجاج", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445" },  
                        { id: 49, name: "بوكس لحم", price: "4000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1" },  
                        { id: 50, name: "بوكس دايت", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1540420773420-3366772f4999" },  
                        { id: 51, name: "دونه ر مشكل جبن", price: "5000 د.ع", img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46" },  
                        { id: 52, name: "فنگر", price: "2000-3000 د.ع", img: "https://images.unsplash.com/photo-1573080496219-bb080dd4f877" },  
                        { id: 53, name: "وجبة فنگر مع فلافل", price: "6000 د.ع", img: "https://images.unsplash.com/photo-1573080496219-bb080dd4f877" }  
                    ]  
                },  
                {  
                    id: "mansaf",  
                    name: "المنسف",  
                    items: [  
                        { id: 54, name: "مريشك سادة", price: "8000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1" },  
                        { id: 55, name: "مريشك كامل", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1" },  
                        { id: 56, name: "منسف ٢ نفر", price: "10000 د.ع", img: "https://images.unsplash.com/photo-1544025162-d76694265947" },  
                        { id: 57, name: "منسف ٣ نفر", price: "15 الف", img: "https://images.unsplash.com/photo-1544025162-d76694265947" },  
                        { id: 58, name: "منسف ٤ نفر", price: "20 الف", img: "https://images.unsplash.com/photo-1544025162-d76694265947" },  
                        { id: 59, name: "منسف ٥ نفر", price: "25 الف", img: "https://images.unsplash.com/photo-1544025162-d76694265947" },  
                        { id: 60, name: "كبسة سعودي", price: "40 الف", img: "https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8" }  
                    ]  
                },  
                {  
                    id: "drinks",  
                    name: "المشروبات",  
                    items: [  
                        { id: 61, name: "ببسي", price: "500 د.ع", img: "https://images.unsplash.com/photo-1622483767028-3f66f32aef97" },  
                        { id: 62, name: "فانتا برتقال", price: "500 د.ع", img: "https://images.unsplash.com/photo-1624513444988-d36321244e39" },  
                        { id: 63, name: "سفن اب", price: "500 د.ع", img: "https://images.unsplash.com/photo-1625772299848-391b6a87d7b3" },  
                        { id: 64, name: "چاي كردي", price: "250 د.ع", img: "https://images.unsplash.com/photo-1576092768241-dec231879fc3" },  
                        { id: 65, name: "ده و كردي", price: "1000 د.ع", img: "https://images.unsplash.com/photo-1541544741938-0af808871cc0" }  
                    ]  
                }  
            ]  
        };  
  
        let menuData = JSON.parse(localStorage.getItem('pizza_delivery_data')) || defaultData;  
        let cart = [];  
        let isAdmin = false;  
  
        function saveData() {  
            localStorage.setItem('pizza_delivery_data', JSON.stringify(menuData));  
        }  
  
        function setLanguage(lang) {  
            document.getElementById('welcome-screen').classList.remove('active');  
            document.getElementById('main-screen').classList.add('active');  
            renderMenu();  
        }  
  
        function renderMenu() {  
            document.getElementById('welcome-logo-img').src = menuData.logo;  
            document.getElementById('header-logo-img').src = menuData.logo;  
  
            const catBar = document.getElementById('categories-bar');  
            catBar.innerHTML = '';  
            const container = document.getElementById('menu-container');  
            container.innerHTML = '';  
  
            menuData.categories.forEach((cat, idx) => {  
                // Category Chip  
                const chip = document.createElement('div');  
                chip.className = `cat-chip ${idx === 0 ? 'active' : ''}`;  
                chip.innerText = cat.name;  
                chip.onclick = () => {  
                    document.querySelectorAll('.cat-chip').forEach(c => c.classList.remove('active'));  
                    chip.classList.add('active');  
                    document.getElementById(`sec-${cat.id}`).scrollIntoView({ behavior: 'smooth' });  
                };  
                catBar.appendChild(chip);  
  
                // Section & Products  
                const sectionDiv = document.createElement('div');  
                sectionDiv.id = `sec-${cat.id}`;  
                sectionDiv.style.marginBottom = '30px';  
                sectionDiv.innerHTML = `<h2 class="section-title">${cat.name}</h2>`;  
  
                const grid = document.createElement('div');  
                grid.className = 'products-grid';  
  
                cat.items.forEach(item => {  
                    const card = document.createElement('div');  
                    card.className = 'product-card';  
                    card.innerHTML = `  
                        <div class="product-img-wrap">  
                            <img src="${item.img}" class="product-img" alt="${item.name}">  
                        </div>  
                        <div class="product-info">  
                            <div>  
                                <div class="product-name">${item.name}</div>  
                                <div class="product-price">${item.price}</div>  
                            </div>  
                            <div class="product-actions">  
                                <button class="btn-add" onclick="addToCart('${item.name}', '${item.price}')">طلب</button>  
                                ${isAdmin ? `<button class="btn-edit-item" onclick="openEditItem(${cat.id},${item.id})"><i class="fa-solid fa-pen"></i></button>` : ''}  
                            </div>  
                        </div>  
                    `;  
                    grid.appendChild(card);  
                });  
  
                sectionDiv.appendChild(grid);  
                container.appendChild(sectionDiv);  
            });  
        }  
  
        function addToCart(name, price) {  
            cart.push({ name, price });  
            updateCartUI();  
        }  
  
        function updateCartUI() {  
            const cartFloat = document.getElementById('cart-float');  
            if (cart.length > 0) {  
                cartFloat.style.display = 'flex';  
                document.getElementById('cart-count').innerText = cart.length;  
                document.getElementById('cart-total').innerText = cart.length * 3000; // تقديري  
            } else {  
                cartFloat.style.display = 'none';  
            }  
        }  
  
        function openCartModal() {  
            document.getElementById('cart-modal').style.display = 'flex';  
            const list = document.getElementById('cart-items-list');  
            list.innerHTML = cart.map(i => `<div style="display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid #333;"><span>${i.name}</span><span>${i.price}</span></div>`).join('');  
        }  
  
        function sendWhatsApp(phone) {  
            const address = document.getElementById('customer-address').value;  
            let text = `مرحباً، أريـد طلب الآتي:%0a`;  
            cart.forEach(i => { text += `- ${i.name} (${i.price})%0a`; });  
            if(address) text += `%0aالعنوان ورقم الهاتف: ${address}`;  
            window.open(`https://wa.me/${phone}?text=${text}`, '_blank');  
        }  
  
        function openAdminModal() {  
            if(isAdmin) {  
                alert('أنت في وضع التعديل بالفعل');  
                return;  
            }  
            document.getElementById('admin-modal').style.display = 'flex';  
        }  
  
        function verifyAdminPin() {  
            const pin = document.getElementById('admin-pin-input').value;  
            if(pin === '30067') {  
                isAdmin = true;  
                document.getElementById('pin-section').style.display = 'none';  
                document.getElementById('admin-controls').style.display = 'block';  
                document.getElementById('admin-badge-indicator').style.display = 'block';  
                renderMenu();  
                alert('تم الدخول بنجاح');  
                closeModal('admin-modal');  
            } else {  
                alert('الرمز غير صحيح');  
            }  
        }  
  
        function openEditItem(catId, itemId) {  
            // بحث وتعديل سريع  
        }  
  
        function changeLogoPrompt() {  
            const url = prompt('أدخل رابط الصورة الجديدة للوجو:');  
            if(url) {  
                menuData.logo = url;  
                saveData();  
                renderMenu();  
            }  
        }  
  
        function closeModal(id) {  
            document.getElementById(id).style.display = 'none';  
        }  
  
        function openLocation() {  
            window.open('https://maps.google.com/?q=37.158360,42.689598', '_blank');  
        }  
    </script>  
</body>  
</html>  
