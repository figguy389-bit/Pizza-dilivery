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
                        { id: 2, name: "بيتزا سجق", price: "3000 د.ع", img: "  
![Image](Attachments/C0FF82E6-AF47-4663-9DF7-E25934375470.png)  
" },  
                        { id: 3, name: "بيتزا تونا", price: "3000 د.ع", img: "  
![Image](Attachments/60241A2D-704A-4329-9D13-D534879075D3.jpeg)  
" },  
                        { id: 4, name: "بيتزا عادى", price: "3000 د.ع", img: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002" },  
                        { id: 5, name: "بيتزا ايطالي", price: "3000 د.ع", img: "  
![Image](Attachments/910C0359-2507-4AB1-8156-7F2F64029183.jpeg)  
<div dir="rtl">" },</div>  
<div dir="rtl">                        { id: 6, name: "بيتزا مريشك", price: "3000 د.ع", img: "</div>  
![Image](Attachments/DF631F18-5323-4B1D-BE56-43D3DC1FAAC1.jpeg)  
<div dir="rtl">" },</div>  
                        { id: 7, name: "بيتزا مارگريتا", price: "3000 د.ع", img: "  
![Image](Attachments/775A4526-0B28-4CC3-91AB-55410818DC23.png)  
" },  
                        { id: 8, name: "لحم بعجين عادى", price: "1000 د.ع", img: "  
![Image](Attachments/25AEED48-C855-43A8-9537-D2BE371E176C.jpeg)  
" },  
                        { id: 9, name: "لحم بعجين دبل", price: "2000 د.ع", img: "  
![Image](Attachments/DA213773-23C8-4F14-99FD-3F2B26ADD5F2.jpeg)  
" },  
                        { id: 10, name: "كاده عادي", price: "1500 د.ع", img: "  
![Image](Attachments/77FA9B2F-F22B-44CF-A824-BED5600D21CA.jpeg)  
" }  
                    ]  
                },  
                {  
                    id: "pizza-vip",  
                    name: "بيتزا VIP",  
                    items: [  
                        { id: 11, name: "بيتزا نوتيلا", price: "4000 د.ع", img: "  
![Image](Attachments/8094EE7E-A479-4EE6-88FE-D26914E1BC84.jpeg)  
" },  
                        { id: 12, name: "بيتزا vip", price: "5000 د.ع", img: "  
![Image](Attachments/7C760147-7C16-4F44-853D-07666DBB8E98.png)  
" },  
                        { id: 13, name: "بيتزا قومبله", price: "15000 د.ع", img: "  
![Image](Attachments/56A34AED-4DB2-43D4-9FAF-DA61CAE4A443.jpeg)  
" },  
                        { id: 14, name: "بيتزا نيف قومبه له", price: "7000 د.ع", img: "  
![Image](Attachments/510418D7-9B0D-4862-8E05-1DD043D8C29E.jpeg)  
" },  
                        { id: 15, name: "بيتزا عادي", price: "4000 د.ع", img: "  
![Image](Attachments/4DE674A8-703F-4AF5-99E2-0F03C1426080.jpeg)  
" },  
                        { id: 16, name: "بيتزا سجق", price: "5000 د.ع", img: "  
![Image](Attachments/FBC83808-CCED-4F9B-837F-04A17EAD09AA.png)  
" },  
                        { id: 17, name: "بيتزا ببروني", price: "5000 د.ع", img: "  
![Image](Attachments/39E85CF0-92C2-4BA6-9F1C-EC5AF0A3600A.jpeg)  
" },  
                        { id: 18, name: "بيتزا مارگريتا", price: "5000 د.ع", img: "  
![Image](Attachments/65AA6D7F-DFCB-4979-AB12-AC5BE9FAA484.jpeg)  
" },  
                        { id: 19, name: "بيتزا ايطالي", price: "5000 د.ع", img: "  
![Image](Attachments/DD5A4727-848C-4C30-8451-0823D89F0B16.jpeg)  
" },  
                        { id: 20, name: "لحم بعجين", price: "2000 د.ع", img: "  
![Image](Attachments/B7FE4E4F-001D-4155-B624-D0414C98F204.jpeg)  
" }  
                    ]  
                },  
                {  
                    id: "grills",  
                    name: "المشاوي",  
                    items: [  
                        { id: 21, name: "نفر كباب لحم", price: "10 الاف", img: "  
  
" },  
![Image](Attachments/9D9791AB-86EF-443F-B0BD-0230AA32E285.jpeg)  
  
                        { id: 22, name: "نصف نفر", price: "5 الاف", img: "  
![Image](Attachments/F11DA6D5-2CCB-4312-9FD7-30C5CFD3E8F6.jpeg)  
" },  
                        { id: 23, name: "نفر كباب دجاج", price: "8000 د.ع", img: "  
![Image](Attachments/92E342A3-5262-44B7-8E5C-3580953865ED.jpeg)  
" },  
                        { id: 24, name: "نفر تكه لحم", price: "10000 د.ع", img: "  
![Image](Attachments/FFA38E4F-5E5E-4887-8ED9-3B5CFE159D6F.jpeg)  
" },  
                        { id: 25, name: "نفر تكة دجاج", price: "8000 د.ع", img: "  
![Image](Attachments/2126DF14-573D-40E7-8402-9CF4BFAA32F2.png)  
" },  
                        { id: 26, name: "نفر ميلاك", price: "10000 د.ع", img: "  
![Image](Attachments/4041AB3E-14A4-4393-A294-52F5E687A810.jpeg)  
" },  
                        { id: 27, name: "نفر مشكل", price: "10000 د.ع", img: "  
![Image](Attachments/08F96CE2-11E2-4EC5-9104-746635D5FBB9.png)  
" },  
                        { id: 28, name: "نفر جەنگ (اجنحه)", price: "10000 د.ع", img: "  
![Image](Attachments/DAA328D6-7885-460E-8521-380C5B27226A.jpeg)  
" },  
                        { id: 29, name: "كيلو كباب لحم", price: "25 الف", img: "  
![Image](Attachments/FA5D7ED2-31E4-4766-92B2-E3B07C82BE63.jpeg)  
" },  
                        { id: 30, name: "كيلو تكه دجاج", price: "25 الف", img: "  
![Image](Attachments/4E0DC44A-BB84-471A-A225-8D10D057D3B1.png)  
" },  
                        { id: 31, name: "كيلو تكه لحم", price: "25 الف", img: "  
![Image](Attachments/95690F36-9013-4E3A-83A7-B53E8556A204.jpeg)  
" },  
                        { id: 32, name: "كيلو مشكل", price: "27 الف", img: "  
![Image](Attachments/4F9C4B4E-C1AE-471F-8889-5783EF47A1E0.png)  
" },  
                        { id: 33, name: "منسف مشاوي", price: "30 الف", img: "  
![Image](Attachments/9CFC0E01-7B8A-4E5B-91D8-85F217439A2B.png)  
" }  
                    ]  
                },  
                {  
                    id: "sandwiches",  
                    name: "اللفات",  
                    items: [  
                        { id: 34, name: "لفه دجاج عادى", price: "1000 د.ع", img: "  
![Image](Attachments/1F402F3E-6B1F-4C25-B839-43C78791C4C6.jpeg)  
" },  
                        { id: 35, name: "لفه سوري دجاج", price: "2000 د.ع", img: "  
![Image](Attachments/838453C1-18B5-42A8-B1CC-781F121898A4.jpeg)  
" },  
                        { id: 36, name: "لفه فلافل", price: "1000 د.ع", img: "  
![Image](Attachments/A8DD6518-7E5D-4BB7-B41A-8AEC4102257A.jpeg)  
" },  
                        { id: 37, name: "ماعون فلافل", price: "5000 د.ع", img: "  
  
![Image](Attachments/9DC6FFF8-ED05-4152-BF2A-CF7E9A76A499.jpeg)  
  
" },  
                        { id: 38, name: "ماعون گص مريشك (دجاج)", price: "10000 د.ع", img: "  
![Image](Attachments/6C2EBE66-9950-4650-88A1-5132D8B31B6C.jpeg)  
" },  
                        { id: 39, name: "نيڤ ماعون گص مريشك (دجاج)", price: "5000 د.ع", img: "  
![Image](Attachments/319DE837-07E9-4158-A0AF-FBA28B6CE1B9.jpeg)  
" },  
                        { id: 40, name: "لفه لحم (گوشت) عادى", price: "2000 د.ع", img: "  
![Image](Attachments/3CD33D8F-C83E-4C5A-B941-1775A161C1F1.jpeg)  
" },  
                        { id: 41, name: "لفه سوري گوشت (لحم)", price: "3000 د.ع", img: "  
![Image](Attachments/562F93B5-F8F7-4FE0-9752-81549A59CF53.jpeg)  
" },  
                        { id: 42, name: "فلافل سوري", price: "3000 د.ع", img: "  
![Image](Attachments/12613CED-D00B-487C-A949-73EBAD3A972C.png)  
" },  
                        { id: 43, name: "برگر لحم (گوشت)", price: "4000 د.ع", img: "  
![Image](Attachments/C25AF5AC-F206-4A49-834C-433918159D09.jpeg)  
" },  
                        { id: 44, name: "برگر مريشك (دجاج)", price: "3000 د.ع", img: "  
![Image](Attachments/25BF951A-3137-45EF-9AB7-F015365447B4.jpeg)  
" },  
                        { id: 45, name: "دبل چيز برگر", price: "5000 د.ع", img: "  
![Image](Attachments/367E4608-56B2-4253-9E4C-3432CF9BC80E.jpeg)  
" },  
                        { id: 46, name: "دونەر مريشك", price: "3000 د.ع", img: "  
![Image](Attachments/F992ADAF-FF5C-45FE-A177-6FB99CE1BEA8.jpeg)  
" },  
                        { id: 47, name: "دونەر گوشت", price: "4000 د.ع", img: "  
![Stoters talabat](Attachments/2DC89F24-AEED-4D0F-B974-8207C94A088B.jpeg)  
" },  
                        { id: 48, name: "بوكس دجاج", price: "3000 د.ع", img: "  
![Image](Attachments/2D6B03C8-05D7-4F6D-A6CC-58119313AD90.jpeg)  
" },  
                        { id: 49, name: "بوكس لحم", price: "4000 د.ع", img: "  
![Image](Attachments/1F3158E3-4640-4166-AC1F-95C7A5BB03C3.jpeg)  
" },  
                        { id: 50, name: "بوكس دايت", price: "3000 د.ع", img: "  
![Image](Attachments/911E0F9E-AADF-4463-ACB4-CBC9D69AAC52.jpeg)  
" },  
                        { id: 51, name: "دونه ر مشكل جبن", price: "5000 د.ع", img: "  
![Image](Attachments/FCD99EC2-95A4-4691-A000-CCBBBD8C3BE5.jpeg)  
" },  
                        { id: 52, name: "فنگر", price: "1000-3000 د.ع", img: "  
![Image](Attachments/D6B3ADD2-473C-404E-9197-BDAC2B57185D.jpeg)  
" },  
                        { id: 53, name: "وجبة فنگر مع فلافل", price: "6000 د.ع", img: "  
![Image](Attachments/67B885CD-27FC-4B87-AAFE-495C735BCF21.jpeg)  
" }  
                    ]  
                },  
                {  
                    id: "mansaf",  
                    name: "المنسف",  
                    items: [  
                        { id: 54, name: "مريشك سادة", price: "8000 د.ع", img: "  
![Image](Attachments/5E366EF4-7546-4B92-9247-5497C88FB15E.jpeg)  
" },  
                        { id: 55, name: "مريشك كامل", price: "10000 د.ع", img: "  
![Image](Attachments/AF5CCA45-D194-40B1-8FB2-77BC83F4B23E.jpeg)  
" },  
                        { id: 56, name: "منسف ٢ نفر", price: "10000 د.ع", img: "  
![Image](Attachments/47BA76D2-F888-43F5-98CA-983150A21E0B.heic)  
" },  
                        { id: 57, name: "منسف ٣ نفر", price: "15 الف", img: "  
  
![Image](Attachments/7072EDFD-7D42-41E1-8FC3-A3464C3D9F0A.jpeg)  
  
" },  
                        { id: 58, name: "منسف ٤ نفر", price: "20 الف", img: "  
![Image](Attachments/22C6A64B-D791-4786-9931-3E9E009101B4.heic)  
" },  
                        { id: 59, name: "منسف ٥ نفر", price: "25 الف", img: "  
![Image](Attachments/A99A7E9E-8C6F-44BC-B76C-F7DD41146F7D.jpeg)  
" },  
                        { id: 60, name: "كبسة سعودي", price: "40 الف", img: "  
![Image](Attachments/700DCA1D-B250-4B9F-BD96-EA787ACD1CF8.jpeg)  
" }  
                    ]  
                },  
                {  
                    id: "drinks",  
                    name: "المشروبات",  
                    items: [  
                        { id: 61, name: "ببسي", price: "500 د.ع", img: "  
![Image](Attachments/A2D7D6ED-D205-455F-A16C-7FE1E59F22CB.jpeg)  
" },  
                        { id: 62, name: "فانتا برتقال", price: "500 د.ع", img: "  
![Image](Attachments/9BCA492C-E67B-4B80-B575-74423E4A14CE.jpeg)  
" },  
                        { id: 63, name: "سفن اب", price: "500 د.ع", img: "  
![REFRESHING LEMON & LIME TASTE](Attachments/964D4E4F-65DD-4E34-8044-7D948BFD800A.jpeg)  
" },  
                        { id: 64, name: "چاي كردي", price: "250 د.ع", img: "  
![Image](Attachments/0300F306-B82D-48D4-83B2-23658AB1D6DA.jpeg)  
" },  
                        { id: 65, name: "ده و كردي", price: "1000 د.ع", img: "  
![Image](Attachments/94160EFC-D2FD-40B8-B251-AC41D0FAE276.png)  
" }  
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
