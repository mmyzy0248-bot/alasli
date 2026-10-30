# alasli
<!DOCTYPE html>    
<html lang="ar" dir="rtl">    
<head>    
    <meta charset="UTF-8">    
    <meta name="viewport" content="width=device-width, initial-scale=1.0">    
    <title>ALASLI - المتجر الأصلي</title>    
    <script src="https://cdn.tailwindcss.com"></script>    
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">    
    <style>    
        body {     
            font-family: 'Cairo', sans-serif;     
            background-color: #0a0a0a;     
            color: #f1f1f1;    
            background-image: linear-gradient(rgba(10, 10, 10, 0.9), rgba(10, 10, 10, 0.95)), url('https://images.unsplash.com/photo-1614027164847-1b28cfe1df60?q=80&w=1000&auto=format&fit=crop');    
            background-size: cover;    
            background-attachment: fixed;    
            background-position: center;    
            -webkit-user-select: none; user-select: none;     
        }    
        .glass { background: rgba(10, 10, 10, 0.85); backdrop-filter: blur(12px); border-bottom: 1px solid #d4af37; }    
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.85); z-index: 50; align-items: center; justify-content: center; }    
        .modal.active { display: flex; }    
        .tab-content { display: none; }    
        .tab-content.active { display: block; }    
        input, textarea, select { -webkit-user-select: auto; user-select: auto; background-color: #1a1a1a; color: #fff; border: 1px solid #333; outline: none; }    
        input:focus, textarea:focus, select:focus { border-color: #d4af37; }    
        .text-gold { color: #d4af37; }    
        .bg-gold { background-color: #d4af37; color: #000; }    
        .border-gold { border-color: #d4af37; }    
        ::-webkit-scrollbar { width: 6px; height: 6px; }    
        ::-webkit-scrollbar-track { background: #111; }    
        ::-webkit-scrollbar-thumb { background: #d4af37; border-radius: 4px; }    
    </style>    
</head>    
<body class="min-h-screen flex flex-col">    
    
    <!-- ================= واجهة العميل ================= -->    
    <div id="customerView" class="flex-1 flex flex-col">    
        <header class="glass sticky top-0 z-40 shadow-lg">    
            <div class="container mx-auto px-4 py-3 flex justify-between items-center">    
                <div class="text-center flex flex-col items-center">    
                    <i class="fa-solid fa-crown text-gold text-lg -mb-1"></i>    
                    <h1 class="text-2xl font-black text-gold tracking-wider drop-shadow-md">ALASLI</h1>    
                </div>    
                <div class="flex gap-4 items-center">    
                    <button onclick="toggleLanguage()" id="langToggleBtn" class="text-gray-300 hover:text-gold font-bold transition px-2 border border-gray-600 rounded-lg text-sm h-8 flex items-center">EN</button>
                    
                    <button onclick="openModal('loginModal')" id="loginBtn" class="text-gray-300 hover:text-white font-bold transition"><i class="fa-solid fa-user-lock text-gold mr-1"></i> <span data-ar="دخول" data-en="Login">دخول</span></button>    
                    
                    <div id="userMenu" class="hidden flex gap-3 md:gap-4 items-center text-sm md:text-base">    
                        <div id="userProfileDisplay" class="flex items-center gap-2 bg-black/50 px-3 py-1 rounded-full border border-gold/50 hidden md:flex">    
                            <span id="userNameDisplay" class="text-gold font-bold text-xs truncate max-w-[80px]"></span>    
                        </div>    
                        <button onclick="openModal('walletModal')" class="text-gold font-bold bg-black/50 px-3 py-1 rounded-full border border-gold hover:bg-black transition"><i class="fa-solid fa-wallet"></i> <span id="walletBalanceDisplay">0</span> <span data-ar="ج" data-en="EGP">ج</span></button>    
                        <button onclick="openModal('ordersModal')" class="text-gray-300 hover:text-white font-bold transition"><i class="fa-solid fa-box-open text-gold mr-1"></i> <span data-ar="طلباتي" data-en="Orders">طلباتي</span></button>    
                        <button onclick="openModal('cartModal')" class="text-white relative hover:scale-110 transition"><i class="fa-solid fa-cart-shopping text-xl text-gold"></i> <span id="cartCount" class="absolute -top-2 -right-2 bg-red-600 text-white rounded-full w-5 h-5 text-xs flex items-center justify-center font-bold">0</span></button>    
                        <button onclick="logout()" class="text-gray-500 hover:text-red-500 transition"><i class="fa-solid fa-sign-out-alt text-lg"></i></button>    
                    </div>    
                </div>    
            </div>    
                
            <div class="bg-black/60 border-b border-gray-800 py-3">    
                <div class="container mx-auto px-4 flex gap-3 overflow-x-auto whitespace-nowrap scrollbar-hide">    
                    <button onclick="filterProducts('الكل')" class="px-5 py-1.5 bg-gold rounded-full font-bold text-sm text-black hover:bg-yellow-600 transition" data-ar="الكل" data-en="All">الكل</button>    
                    <button onclick="filterProducts('ساعات')" class="px-5 py-1.5 bg-gray-900 border border-gray-700 rounded-full hover:border-gold text-sm transition text-white" data-ar="ساعات" data-en="Watches">ساعات</button>    
                    <button onclick="filterProducts('خواتم')" class="px-5 py-1.5 bg-gray-900 border border-gray-700 rounded-full hover:border-gold text-sm transition text-white" data-ar="خواتم" data-en="Rings">خواتم</button>    
                    <button onclick="filterProducts('سلاسل')" class="px-5 py-1.5 bg-gray-900 border border-gray-700 rounded-full hover:border-gold text-sm transition text-white" data-ar="سلاسل" data-en="Chains">سلاسل</button>    
                    <button onclick="filterProducts('انسيالات')" class="px-5 py-1.5 bg-gray-900 border border-gray-700 rounded-full hover:border-gold text-sm transition text-white" data-ar="انسيالات" data-en="Bracelets">انسيالات</button>    
                    <button onclick="filterProducts('برفانات')" class="px-5 py-1.5 bg-gray-900 border border-gray-700 rounded-full hover:border-gold text-sm transition text-white" data-ar="برفانات" data-en="Perfumes">برفانات</button>    
                    <button onclick="filterProducts('مكياج')" class="px-5 py-1.5 bg-gray-900 border border-gray-700 rounded-full hover:border-gold text-sm transition text-white" data-ar="مكياج" data-en="Makeup">مكياج</button>    
                    <button onclick="filterProducts('روج')" class="px-5 py-1.5 bg-gray-900 border border-gray-700 rounded-full hover:border-gold text-sm transition text-white" data-ar="روج" data-en="Lipstick">روج</button>    
                </div>    
            </div>    
        </header>    
    
        <main class="container mx-auto px-4 py-8 flex-1">    
            <div id="productsGrid" class="grid grid-cols-2 md:grid-cols-4 gap-4 md:gap-6"></div>    
        </main>    
    
        <footer id="secretFooter" class="text-center py-6 text-gray-600 text-xs mt-auto cursor-pointer border-t border-gray-800 bg-black/50 hover:text-gray-400 transition" data-ar="جميع الحقوق محفوظة لمتجر ALASLI &copy; 2026" data-en="All rights reserved to ALASLI Store &copy; 2026">    
            جميع الحقوق محفوظة لمتجر ALASLI &copy; 2026    
        </footer>    
    
        <!-- الشات الذكي -->    
        <div id="aiChat" class="hidden fixed bottom-24 left-4 md:left-20 w-[90vw] md:w-80 bg-gray-900 rounded-xl shadow-2xl border border-gold z-50 flex flex-col overflow-hidden">    
            <div class="bg-gold text-black p-4 font-bold flex justify-between items-center">    
                <span><i class="fa-solid fa-headset mr-1"></i> <span data-ar="المساعد الذكي" data-en="Smart Assistant">المساعد الذكي</span></span>    
                <button onclick="document.getElementById('aiChat').classList.add('hidden')" class="text-xl hover:text-white transition"><i class="fa-solid fa-times"></i></button>    
            </div>    
            <div id="chatMessages" class="p-4 h-64 overflow-y-auto flex flex-col gap-3 text-sm bg-gray-900">    
                <div class="bg-gray-800 border border-gray-700 text-gray-200 p-3 rounded-xl rounded-tr-none self-start shadow" data-ar="مرحباً بك في متجر ALASLI الفاخر! كيف يمكنني مساعدتك؟" data-en="Welcome to ALASLI! How can I help you?">مرحباً بك في متجر ALASLI الفاخر! كيف يمكنني مساعدتك؟</div>    
            </div>    
            <div class="p-3 border-t border-gray-800 flex gap-2 bg-black">    
                <input type="text" id="chatInput" class="flex-1 bg-gray-800 border border-gray-700 rounded-lg px-3 py-2 text-sm text-white focus:border-gold transition" data-placeholder-ar="اكتب استفسارك هنا..." data-placeholder-en="Type your message..." placeholder="اكتب استفسارك هنا...">    
                <button onclick="sendChatMessage()" class="bg-gold text-black px-4 py-2 rounded-lg font-bold hover:bg-yellow-600 transition"><i class="fa-solid fa-paper-plane"></i></button>    
            </div>    
        </div>    
    
        <!-- ================= نافذة تسجيل الدخول / إنشاء حساب / نسيت كلمة المرور ================= -->    
        <div id="loginModal" class="modal">    
            <div class="bg-gray-900 border border-gold p-6 rounded-2xl w-[90%] md:w-96 relative shadow-2xl">    
                <button onclick="closeModal('loginModal')" class="absolute top-4 left-4 text-gray-500 hover:text-white text-xl transition"><i class="fa-solid fa-times"></i></button>    
                <div class="text-center mb-4">  
                    <i class="fa-solid fa-crown text-4xl text-gold mb-2 drop-shadow-md"></i>    
                    <h2 class="text-xl font-bold text-white" id="authModalTitle" data-ar="تسجيل الدخول" data-en="Login">تسجيل الدخول</h2>    
                </div>  

                <!-- نموذج تسجيل الدخول العادي -->
                <div id="loginFormSection" class="flex flex-col gap-3">    
                    <input type="email" id="authEmail" data-placeholder-ar="البريد الإلكتروني" data-placeholder-en="Email Address" placeholder="البريد الإلكتروني" class="w-full bg-black border border-gray-700 p-3 rounded-xl text-sm text-white focus:border-gold" dir="ltr">  
                    <input type="password" id="authPassword" data-placeholder-ar="كلمة المرور" data-placeholder-en="Password" placeholder="كلمة المرور" class="w-full bg-black border border-gray-700 p-3 rounded-xl text-sm text-white focus:border-gold" dir="ltr">  
                      
                    <button onclick="handleUserLogin()" class="w-full bg-gold hover:bg-yellow-600 text-black py-3 rounded-xl font-bold shadow-lg transition" data-ar="دخول" data-en="Sign In">دخول</button>  
                    
                    <div class="flex justify-between items-center text-xs mt-2 text-gray-400">  
                        <button onclick="showRegisterView()" class="hover:text-gold transition underline" data-ar="إنشاء حساب جديد" data-en="Create Account">إنشاء حساب جديد</button>  
                        <button onclick="showForgotView()" class="hover:text-red-400 transition" data-ar="نسيت كلمة المرور؟" data-en="Forgot Password?">نسيت كلمة المرور؟</button>  
                    </div>  
                </div>  

                <!-- نموذج إنشاء حساب جديد -->
                <div id="registerFormSection" class="hidden flex flex-col gap-3">    
                    <input type="text" id="regName" data-placeholder-ar="الاسم الكريم" data-placeholder-en="Full Name" placeholder="الاسم الكريم" class="w-full bg-black border border-gray-700 p-3 rounded-xl text-sm text-white focus:border-gold">  
                    <input type="email" id="regEmail" data-placeholder-ar="البريد الإلكتروني" data-placeholder-en="Email Address" placeholder="البريد الإلكتروني" class="w-full bg-black border border-gray-700 p-3 rounded-xl text-sm text-white focus:border-gold" dir="ltr">  
                    <input type="password" id="regPassword" data-placeholder-ar="كلمة المرور الجديدة" data-placeholder-en="New Password" placeholder="كلمة المرور الجديدة" class="w-full bg-black border border-gray-700 p-3 rounded-xl text-sm text-white focus:border-gold" dir="ltr">  
                      
                    <button onclick="handleUserRegister()" class="w-full bg-gold hover:bg-yellow-600 text-black py-3 rounded-xl font-bold shadow-lg transition" data-ar="إتمام التسجيل" data-en="Register Now">إتمام التسجيل</button>  
                    <div class="text-center mt-2">  
                        <button onclick="showLoginView()" class="text-xs text-gray-400 hover:text-gold transition underline" data-ar="الرجوع لتسجيل الدخول" data-en="Back to Login">الرجوع لتسجيل الدخول</button>  
                    </div>  
                </div>  

                <!-- نموذج نسيت كلمة المرور -->
                <div id="forgotFormSection" class="hidden flex flex-col gap-3">    
                    <p class="text-xs text-gray-300 text-center" data-ar="أدخل بريدك الإلكتروني لتوليد رمز التحقق (OTP) وتغيير كلمة المرور." data-en="Enter email to receive OTP code.">أدخل بريدك الإلكتروني لتوليد رمز التحقق (OTP) وتغيير كلمة المرور.</p>  
                    <input type="email" id="forgotEmail" data-placeholder-ar="البريد الإلكتروني المسجل" data-placeholder-en="Registered Email" placeholder="البريد الإلكتروني المسجل" class="w-full bg-black border border-gray-700 p-3 rounded-xl text-sm text-white focus:border-gold" dir="ltr">  
                    
                    <div id="forgotStep1">  
                        <button onclick="sendOtpCode()" class="w-full bg-gold hover:bg-yellow-600 text-black py-3 rounded-xl font-bold shadow-lg transition" data-ar="إرسال كود التحقق" data-en="Send Code">إرسال كود التحقق</button>  
                    </div>  

                    <div id="forgotStep2" class="hidden flex flex-col gap-3">  
                        <input type="text" id="otpInput" data-placeholder-ar="أدخل الكود المكون من 4 أرقام" data-placeholder-en="Enter 4-digit code" placeholder="أدخل الكود المكون من 4 أرقام" class="w-full bg-black border border-gold p-3 rounded-xl text-sm text-white text-center tracking-widest font-bold">  
                        <input type="password" id="newPasswordInput" data-placeholder-ar="كلمة المرور الجديدة" data-placeholder-en="New Password" placeholder="كلمة المرور الجديدة" class="w-full bg-black border border-gray-700 p-3 rounded-xl text-sm text-white focus:border-gold" dir="ltr">  
                        <button onclick="verifyAndResetPassword()" class="w-full bg-green-600 hover:bg-green-700 text-white py-3 rounded-xl font-bold shadow-lg transition" data-ar="تأكيد وتغيير كلمة المرور" data-en="Confirm & Change">تأكيد وتغيير كلمة المرور</button>  
                    </div>  

                    <div class="text-center mt-2">  
                        <button onclick="showLoginView()" class="text-xs text-gray-400 hover:text-gold transition underline" data-ar="الرجوع لتسجيل الدخول" data-en="Back to Login">الرجوع لتسجيل الدخول</button>  
                    </div>  
                </div>  

            </div>    
        </div>    
    
        <!-- نافذة المحفظة -->    
        <div id="walletModal" class="modal">    
            <div class="bg-gray-900 border border-gray-700 p-6 rounded-2xl w-[90%] md:w-96 relative shadow-2xl">    
                <button onclick="closeModal('walletModal')" class="absolute top-4 left-4 text-gray-500 hover:text-white text-xl transition"><i class="fa-solid fa-times"></i></button>    
                <div class="text-center mb-6 border-b border-gray-800 pb-4">    
                    <h2 class="text-xl font-bold text-white mb-4"><i class="fa-solid fa-wallet text-gold"></i> <span data-ar="رصيد المحفظة" data-en="Wallet Balance">رصيد المحفظة</span></h2>    
                    <div class="bg-black/50 border border-gold p-4 rounded-xl inline-block min-w-[200px] shadow-inner">    
                        <div class="text-3xl font-black text-gold drop-shadow-md" id="modalWalletBalance">0 <span class="text-sm" data-ar="ج.م" data-en="EGP">ج.م</span></div>    
                    </div>    
                </div>    
                <div class="bg-gray-800 p-4 rounded-xl border border-gray-700 text-center">    
                    <div class="flex justify-center mb-3">    
                        <div class="bg-red-600 p-3 rounded-2xl shadow-lg border-2 border-red-500 flex items-center justify-center">    
                            <span class="text-white font-black text-xl tracking-tighter">VODAFONE</span>  
                        </div>    
                    </div>    
                    <h3 class="font-bold text-lg text-white mb-3" data-ar="إيداع فودافون كاش" data-en="Vodafone Cash Deposit">إيداع فودافون كاش</h3>    
                    <div class="text-xs text-gray-300 mb-4 bg-black/60 p-3 rounded-lg border border-gray-700">    
                        <span data-ar="حول المبلغ لأحد الأرقام المعتمدة:" data-en="Transfer amount to certified numbers:">حول المبلغ لأحد الأرقام المعتمدة:</span><br>    
                        <span class="font-bold text-red-500 text-lg tracking-widest inline-block mt-2">01097423486</span><br><span data-ar="أو" data-en="or">أو</span><br>    
                        <span class="font-bold text-red-500 text-lg tracking-widest inline-block mt-1">01210922383</span>    
                    </div>    
                    <input type="tel" id="walletPhone" data-placeholder-ar="رقم الموبايل المحول منه" data-placeholder-en="Sender Mobile Number" placeholder="رقم الموبايل المحول منه" class="w-full bg-black border border-gray-600 p-3 rounded-lg mb-3 text-sm text-white focus:border-red-500 text-center">    
                    <input type="number" id="walletAmount" data-placeholder-ar="المبلغ المحول" data-placeholder-en="Amount Sent" placeholder="المبلغ المحول" class="w-full bg-black border border-gray-600 p-3 rounded-lg mb-4 text-sm text-white focus:border-red-500 text-center">    
                    <button onclick="submitWalletRequest()" class="w-full bg-red-600 hover:bg-red-700 text-white py-3 rounded-lg font-bold shadow-lg transition"><i class="fa-solid fa-paper-plane mr-2"></i> <span data-ar="إرسال طلب الشحن" data-en="Send Request">إرسال طلب الشحن</span></button>    
                </div>    
            </div>    
        </div>    
    
        <!-- السلة -->    
        <div id="cartModal" class="modal">    
            <div class="bg-gray-900 border border-gray-700 p-6 rounded-2xl w-[95%] md:w-full max-w-lg max-h-[90vh] overflow-y-auto relative shadow-2xl">    
                <button onclick="closeModal('cartModal')" class="absolute top-4 left-4 text-gray-500 hover:text-white text-xl transition"><i class="fa-solid fa-times"></i></button>    
                <h2 class="text-xl font-bold mb-5 border-b border-gray-800 pb-3 text-gold"><i class="fa-solid fa-cart-shopping"></i> <span data-ar="سلة المشتريات" data-en="Shopping Cart">سلة المشتريات</span></h2>    
                    
                <div id="cartItems" class="flex flex-col gap-3 mb-5 min-h-[80px]"></div>    
                    
                <div class="bg-black/50 p-4 rounded-xl border border-gray-700 mb-5 flex justify-between items-center">    
                    <span class="font-bold text-gray-300" data-ar="الإجمالي الكلي:" data-en="Total:">الإجمالي الكلي:</span>    
                    <span class="font-black text-2xl text-gold"><span id="cartTotal">0</span> <span data-ar="ج.م" data-en="EGP">ج.م</span></span>    
                </div>    
    
                <div class="space-y-3 mb-6 bg-gray-800 p-4 rounded-xl border border-gray-700">    
                    <h3 class="text-sm font-bold text-white mb-2"><i class="fa-solid fa-truck-fast text-gold mr-1"></i> <span data-ar="عنوان وتفاصيل التوصيل" data-en="Shipping Details">عنوان وتفاصيل التوصيل</span></h3>    
                    <div class="grid grid-cols-2 gap-3">    
                        <select id="checkoutGov" class="w-full bg-black border border-gray-600 p-3 rounded-lg text-sm text-white focus:border-gold" onchange="updateCities()">    
                            <option value="" data-ar="المحافظة" data-en="Governorate">المحافظة</option>    
                            <option value="القاهرة">القاهرة / Cairo</option><option value="الدقهلية">الدقهلية / Dakahlia</option>    
                            <option value="الشرقية">الشرقية / Sharqia</option><option value="الإسكندرية">الإسكندرية / Alex</option>    
                            <option value="الجيزة">الجيزة / Giza</option>    
                        </select>    
                        <select id="checkoutCity" class="w-full bg-black border border-gray-600 p-3 rounded-lg text-sm text-white focus:border-gold">    
                            <option value="" data-ar="المركز/المدينة" data-en="City">المركز/المدينة</option>    
                        </select>    
                    </div>    
                    <textarea id="checkoutAddress" data-placeholder-ar="الشارع ورقم العمارة والشقة..." data-placeholder-en="Street, Building, Flat..." placeholder="الشارع ورقم العمارة والشقة..." class="w-full bg-black border border-gray-600 p-3 rounded-lg text-sm text-white focus:border-gold resize-none h-16"></textarea>    
                    <input type="tel" id="checkoutPhone" data-placeholder-ar="رقم الهاتف للتواصل" data-placeholder-en="Contact Phone" placeholder="رقم الهاتف للتواصل" class="w-full bg-black border border-gray-600 p-3 rounded-lg text-sm text-white focus:border-gold">    
                </div>    
                <button onclick="checkout()" class="w-full bg-gold hover:bg-yellow-600 text-black py-4 rounded-xl font-bold text-lg shadow-lg transition"><i class="fa-solid fa-check-circle mr-2"></i> <span data-ar="تأكيد الطلب والدفع" data-en="Confirm Order & Pay">تأكيد الطلب والدفع</span></button>    
            </div>    
        </div>    
    
        <!-- سجل الطلبات -->    
        <div id="ordersModal" class="modal">    
            <div class="bg-gray-900 border border-gray-700 p-6 rounded-2xl w-[95%] md:w-full max-w-lg max-h-[85vh] overflow-y-auto relative shadow-2xl">    
                <button onclick="closeModal('ordersModal')" class="absolute top-4 left-4 text-gray-500 hover:text-white text-xl transition"><i class="fa-solid fa-times"></i></button>    
                <h2 class="text-xl font-bold mb-5 border-b border-gray-800 pb-3 text-gold"><i class="fa-solid fa-box-open"></i> <span data-ar="سجل طلباتي" data-en="My Orders History">سجل طلباتي</span></h2>    
                <div id="myOrdersList" class="flex flex-col gap-4"></div>    
            </div>    
        </div>    

        <!-- ================= نافذة نجاح الطلب (علامة صح ✔️) ================= -->
        <div id="successModal" class="modal">
            <div class="bg-gray-900 border border-green-500 p-8 rounded-3xl w-[90%] md:w-96 text-center shadow-[0_0_40px_rgba(34,197,94,0.3)] relative">
                <button onclick="closeModal('successModal')" class="absolute top-4 left-4 text-gray-500 hover:text-white text-xl transition"><i class="fa-solid fa-times"></i></button>
                
                <div class="w-24 h-24 bg-green-600/20 rounded-full flex items-center justify-center mx-auto mb-5 border-4 border-green-500 shadow-[0_0_20px_rgba(34,197,94,0.5)]">
                    <i class="fa-solid fa-check text-5xl text-green-500 drop-shadow-md"></i>
                </div>
                
                <h2 class="text-3xl font-black text-white mb-2 tracking-wide" data-ar="تم طلبك بنجاح!" data-en="Order Placed!">تم طلبك بنجاح!</h2>
                <p class="text-sm text-gray-400 mb-5" data-ar="تم استلام طلبك وجاري تجهيزه." data-en="Your order has been received and is being prepared.">تم استلام طلبك وجاري تجهيزه.</p>
                
                <div class="bg-black/50 p-4 rounded-xl border border-gray-800 mb-6 text-right" dir="auto">
                    <div class="flex justify-between items-center mb-2">
                        <span class="text-gray-400 text-sm" data-ar="كود الطلب:" data-en="Order ID:">كود الطلب:</span>
                        <span id="successOrderId" class="text-gold font-bold tracking-wider"></span>
                    </div>
                    <div class="flex justify-between items-center border-t border-gray-800 pt-2">
                        <span class="text-gray-400 text-sm" data-ar="المبلغ المخصوم:" data-en="Deducted Amount:">المبلغ المخصوم:</span>
                        <span class="text-red-400 font-bold"><span id="successOrderTotal"></span> <span data-ar="ج.م" data-en="EGP">ج.م</span></span>
                    </div>
                </div>
                
                <button onclick="closeModal('successModal'); openModal('ordersModal')" class="w-full bg-gold hover:bg-yellow-600 text-black py-3 rounded-xl font-bold shadow-lg transition text-lg"><i class="fa-solid fa-list-check mr-2"></i> <span data-ar="متابعة حالة الطلب" data-en="Track Order">متابعة حالة الطلب</span></button>
            </div>
        </div>
    
        <!-- عارض الصور Lightbox -->    
        <div id="lightboxModal" class="modal">    
            <div class="relative w-full h-full md:max-w-xl flex items-center justify-center p-4">    
                <button onclick="closeModal('lightboxModal')" class="absolute top-6 right-6 text-white text-3xl z-50 bg-black/50 w-12 h-12 rounded-full hover:bg-red-600 transition border border-gray-600"><i class="fa-solid fa-times"></i></button>    
                <img id="lightboxImage" src="" class="max-w-full max-h-[80vh] rounded-xl shadow-2xl object-contain border-2 border-gold bg-black">    
                <div class="absolute inset-y-0 left-4 flex items-center"><button onclick="changeLightboxImage(-1)" class="bg-black/80 border border-gold text-gold w-12 h-12 rounded-full flex items-center justify-center hover:bg-gold hover:text-black transition"><i class="fa-solid fa-chevron-left text-xl"></i></button></div>    
                <div class="absolute inset-y-0 right-4 flex items-center"><button onclick="changeLightboxImage(1)" class="bg-black/80 border border-gold text-gold w-12 h-12 rounded-full flex items-center justify-center hover:bg-gold hover:text-black transition"><i class="fa-solid fa-chevron-right text-xl"></i></button></div>    
                <div id="lightboxDots" class="absolute bottom-10 left-0 right-0 flex justify-center gap-3"></div>    
            </div>    
        </div>    
    </div>    
    
    <!-- ================= شاشة دخول الإدارة السريّة ================= -->    
    <div id="adminLoginScreen" class="hidden fixed inset-0 bg-black/95 z-50 flex items-center justify-center p-4">    
        <div class="bg-gray-900 border border-gold p-8 rounded-2xl shadow-2xl w-full max-w-sm text-center relative">    
            <button onclick="closeAdminLogin()" class="absolute top-4 left-4 text-gray-500 hover:text-white text-xl"><i class="fa-solid fa-times"></i></button>    
            <div class="mb-6"><i class="fa-solid fa-shield-halved text-5xl text-gold mb-2"></i><h2 class="text-2xl font-black text-white">الإدارة السريّة</h2></div>    
            <input type="email" id="adminEmail" placeholder="البريد الإلكتروني" class="w-full bg-black border border-gray-700 p-3 rounded-lg mb-4 text-left text-white focus:border-gold" dir="ltr">    
            <input type="password" id="adminPassword" placeholder="كلمة المرور" class="w-full bg-black border border-gray-700 p-3 rounded-lg mb-6 text-left text-white focus:border-gold" dir="ltr">    
            <button onclick="loginAdmin()" class="w-full bg-gold hover:bg-yellow-600 text-black py-3 rounded-lg font-bold text-lg"><i class="fa-solid fa-lock-open mr-2"></i> دخول</button>    
        </div>    
    </div>    
    
    <!-- ================= لوحة تحكم الإدارة (العربية دائماً) ================= -->    
    <div id="adminDashboard" class="hidden h-screen w-full bg-gray-900 flex flex-col md:flex-row overflow-hidden fixed inset-0 z-50 text-white" dir="rtl">    
        <div class="w-full md:w-64 bg-black border-l border-gray-800 flex md:flex-col overflow-x-auto md:overflow-visible shadow-xl z-10 shrink-0">    
            <div class="p-6 font-black text-gold text-2xl text-center border-b border-gray-800 hidden md:block"><i class="fa-solid fa-crown text-sm block mb-1"></i> ALASLI ADMIN</div>    
            <button onclick="switchTab('products')" class="p-4 hover:bg-gray-800 text-gray-300 hover:text-gold whitespace-nowrap flex-1 md:flex-none text-center md:text-right border-b md:border-b-0 border-gray-800 transition"><i class="fa-solid fa-box md:ml-2 block md:inline"></i> المنتجات</button>    
            <button onclick="switchTab('orders')" class="p-4 hover:bg-gray-800 text-gray-300 hover:text-gold whitespace-nowrap flex-1 md:flex-none text-center md:text-right border-b md:border-b-0 border-gray-800 transition"><i class="fa-solid fa-list-check md:ml-2 block md:inline"></i> الطلبات</button>    
            <button onclick="switchTab('wallet')" class="p-4 hover:bg-gray-800 text-gray-300 hover:text-gold whitespace-nowrap flex-1 md:flex-none text-center md:text-right border-b md:border-b-0 border-gray-800 transition"><i class="fa-solid fa-wallet md:ml-2 block md:inline"></i> المحافظ</button>    
            <button onclick="switchTab('security')" class="p-4 hover:bg-gray-800 text-gray-300 hover:text-gold whitespace-nowrap flex-1 md:flex-none text-center md:text-right border-b md:border-b-0 border-gray-800 transition"><i class="fa-solid fa-shield md:ml-2 block md:inline"></i> الأمان</button>    
            <button onclick="exitAdmin()" class="p-4 bg-red-900/30 hover:bg-red-600 text-red-400 hover:text-white whitespace-nowrap md:mt-auto flex-1 md:flex-none text-center md:text-right border-t border-gray-800 transition"><i class="fa-solid fa-power-off md:ml-2 block md:inline"></i> إغلاق الإدارة</button>    
        </div>    
    
        <div class="flex-1 overflow-y-auto p-4 md:p-8 pb-20 bg-gray-900/50">    
            <!-- تاب إضافة وتعديل المنتجات -->    
            <div id="tab-products" class="tab-content active">    
                <h2 class="text-2xl font-bold mb-6 text-gold"><i class="fa-solid fa-plus-circle"></i> إضافة منتج جديد</h2>    
                <div class="bg-gray-800 p-6 rounded-2xl shadow-lg border border-gray-700 mb-8 grid grid-cols-1 md:grid-cols-2 gap-5">    
                    <div><label class="block text-xs text-gray-400 mb-1">اسم المنتج</label><input type="text" id="pName" placeholder="أدخل اسم المنتج..." class="w-full bg-black border border-gray-700 p-3 rounded-lg focus:border-gold"></div>    
                    <div><label class="block text-xs text-gray-400 mb-1">القسم</label><select id="pCategory" class="w-full bg-black border border-gray-700 p-3 rounded-lg focus:border-gold text-white"><option value="ساعات">ساعات</option><option value="خواتم">خواتم</option><option value="سلاسل">سلاسل</option><option value="انسيالات">انسيالات</option><option value="برفانات">برفانات</option><option value="مكياج">مكياج</option><option value="روج">روج</option></select></div>    
                    <div class="md:col-span-2"><label class="block text-xs text-gray-400 mb-1">الوصف والتفاصيل</label><textarea id="pDesc" placeholder="اكتب وصف جذاب..." class="w-full bg-black border border-gray-700 p-3 rounded-lg focus:border-gold resize-none h-20 text-sm"></textarea></div>    
                    <div><label class="block text-xs text-gray-400 mb-1">التكلفة (ج.م)</label><input type="number" id="pCost" class="w-full bg-black border border-gray-700 p-3 rounded-lg focus:border-gold" oninput="calcPrice()"></div>    
                    <div><label class="block text-xs text-gray-400 mb-1">المكسب %</label><input type="number" id="pMargin" class="w-full bg-black border border-gray-700 p-3 rounded-lg focus:border-gold" value="20" oninput="calcPrice()"></div>    
                    <div class="md:col-span-2 text-center bg-black/60 border border-gold/50 p-4 rounded-xl"><span class="text-sm text-gray-400 block mb-1">السعر النهائي للبيع</span><span id="pFinalPrice" class="text-3xl font-black text-gold">0</span> <span class="text-gold text-sm">ج.م</span></div>    
                    <div class="md:col-span-2 bg-black/40 p-4 rounded-xl border border-gray-700"><label class="text-sm font-bold block mb-2 text-gray-300"><i class="fa-solid fa-images text-gold mr-1"></i> صور (حتى 5)</label><input type="file" id="pImages" multiple accept="image/*" class="w-full border border-gray-700 p-2 rounded-lg text-sm text-gray-400 file:mr-4 file:py-2 file:px-4 file:rounded-lg file:bg-gold file:text-black" onchange="previewImages()"><div id="imagePreviews" class="flex gap-3 mt-4 overflow-x-auto pb-2"></div></div>    
                    <button onclick="addProduct()" class="md:col-span-2 bg-gold hover:bg-yellow-600 text-black py-4 rounded-xl font-bold text-lg shadow-lg"><i class="fa-solid fa-cloud-arrow-up mr-2"></i> حفظ ونشر</button>    
                </div>    
                    
                <h2 class="text-xl font-bold mb-4 text-white border-b border-gray-800 pb-2"><i class="fa-solid fa-box-open text-gold mr-1"></i> المنتجات الحالية (للإدارة)</h2>    
                <div id="adminProductsList" class="grid grid-cols-2 md:grid-cols-4 gap-5"></div>    
            </div>    
    
            <div id="tab-orders" class="tab-content">    
                <h2 class="text-2xl font-bold mb-6 text-gold"><i class="fa-solid fa-clipboard-list"></i> سجل الطلبات (بالصور التفصيلية)</h2>    
                <input type="text" id="orderSearch" placeholder="بحث برقم الطلب (#ORD-)..." class="w-full bg-black border border-gray-700 p-4 rounded-xl mb-6 focus:border-gold text-white" onkeyup="renderAdminOrders()">    
                <div id="adminOrdersList" class="flex flex-col gap-4"></div>    
            </div>    
                
            <div id="tab-wallet" class="tab-content">    
                <h2 class="text-2xl font-bold mb-6 text-gold"><i class="fa-solid fa-money-bill-transfer"></i> مراجعة تحويلات فودافون كاش</h2>    
                <div id="adminWalletList" class="flex flex-col gap-4"></div>    
            </div>    
                
            <div id="tab-security" class="tab-content">    
                <h2 class="text-2xl font-bold mb-6 text-gold"><i class="fa-solid fa-shield-halved"></i> الأمان</h2>    
                <div class="bg-gray-800 border border-gray-700 p-6 rounded-2xl shadow-lg max-w-md">    
                    <label class="block text-sm text-gray-400 mb-2">الإيميل</label><input type="email" id="newAdminEmail" class="w-full bg-black border border-gray-700 p-3 rounded-lg mb-5 text-white focus:border-gold" dir="ltr">    
                    <label class="block text-sm text-gray-400 mb-2">كلمة المرور الجديدة</label><input type="password" id="newAdminPassword" class="w-full bg-black border border-gray-700 p-3 rounded-lg mb-6 text-white focus:border-gold" dir="ltr">    
                    <button onclick="updateCredentials()" class="w-full bg-gold hover:bg-yellow-600 text-black py-3 rounded-xl font-bold shadow-lg"><i class="fa-solid fa-floppy-disk mr-2"></i> حفظ</button>    
                </div>    
            </div>    
        </div>    
    </div>    
    
    <!-- ================= كود الجافاسكربت ================= -->    
    <script>    
        const i18n = {
            ar: {
                fillFields: 'الرجاء تعبئة جميع الحقول!',
                invalidEmail: 'أدخل بريد إلكتروني صحيح!',
                emailExists: 'هذا البريد مسجل مسبقاً! قم بتسجيل الدخول مباشرة.',
                accCreated: 'تم إنشاء الحساب بنجاح! تم تسجيل دخولك تلقائياً.',
                enterCredentials: 'الرجاء إدخال البريد الإلكتروني وكلمة المرور.',
                notRegistered: 'هذا البريد غير مسجل! انشئ حساباً جديداً أولاً.',
                wrongPass: 'كلمة المرور غير صحيحة!',
                enterEmailFirst: 'أدخل البريد الإلكتروني أولاً.',
                emailNotStore: 'هذا البريد غير مسجل في المتجر!',
                otpSent: 'رمز التحقق الخاص بك هو:',
                wrongOtp: 'كود التحقق غير صحيح!',
                shortPass: 'كلمة المرور يجب ألا تقل عن 4 أحرف/أرقام.',
                passChanged: 'تم تغيير كلمة المرور بنجاح! يمكنك تسجيل الدخول بها الآن.',
                cartEmpty: 'السلة فارغة!',
                enterAddress: 'الرجاء إدخال بيانات العنوان ورقم الهاتف بالكامل.',
                noBalance: 'عفواً، رصيد المحفظة غير كافٍ. يرجى شحن المحفظة أولاً.',
                fillTransfer: 'أكمل بيانات التحويل',
                transferSent: 'تم إرسال طلب الشحن.',
                copied: 'تم النسخ',
                egp: 'ج.م',
                pcs: 'قطع',
                emptyProducts: 'لا توجد منتجات متاحة حالياً.',
                orderSuccess: 'تم تأكيد طلبك بنجاح!',
                checkoutError: 'حدث خطأ أثناء معالجة الطلب، يرجى المحاولة مرة أخرى.'
            },
            en: {
                fillFields: 'Please fill all fields!',
                invalidEmail: 'Enter a valid email address!',
                emailExists: 'Email already registered! Please login directly.',
                accCreated: 'Account created successfully! You are logged in.',
                enterCredentials: 'Please enter email and password.',
                notRegistered: 'Email not registered! Create an account first.',
                wrongPass: 'Incorrect password!',
                enterEmailFirst: 'Enter email address first.',
                emailNotStore: 'This email is not registered in the store!',
                otpSent: 'Your verification code is:',
                wrongOtp: 'Incorrect verification code!',
                shortPass: 'Password must be at least 4 characters/digits.',
                passChanged: 'Password changed successfully! You can login now.',
                cartEmpty: 'Cart is empty!',
                enterAddress: 'Please enter full address and phone number.',
                noBalance: 'Insufficient wallet balance. Please recharge first.',
                fillTransfer: 'Complete transfer details',
                transferSent: 'Transfer request sent.',
                copied: 'Copied',
                egp: 'EGP',
                pcs: 'pcs',
                emptyProducts: 'No products available currently.',
                orderSuccess: 'Order confirmed successfully!',
                checkoutError: 'An error occurred while processing the order. Please try again.'
            }
        };

        const catMap = { 'ساعات': 'Watches', 'خواتم': 'Rings', 'سلاسل': 'Chains', 'انسيالات': 'Bracelets', 'برفانات': 'Perfumes', 'مكياج': 'Makeup', 'روج': 'Lipstick' };

        const egyptData = {    
            "القاهرة": ["مدينة نصر", "المعادي", "مصر الجديدة", "شبرا", "التجمع الخامس", "وسط البلد"],    
            "الدقهلية": ["المنصورة", "طلخا", "شربين", "ميت غمر", "دكرنس", "بلقاس"],    
            "الشرقية": ["الزقازيق", "منيا القمح", "فاقوس", "بلبيس", "أبو كبير"],    
            "الإسكندرية": ["سموحة", "ميامي", "سيدي بشر", "المنتزه", "برج العرب"],    
            "الجيزة": ["المهندسين", "الدقي", "الهرم", "فيصل", "الشيخ زايد"]    
        };    
            
        let currentUser = JSON.parse(localStorage.getItem('alasli_currentUser'));    
        let products = JSON.parse(localStorage.getItem('alasli_products')) || [];    
        let cart = [];    
        let currentLightboxImages = [], currentLightboxIndex = 0;    
        let currentFilter = 'الكل';    
        let adminCreds = JSON.parse(localStorage.getItem('alasli_admin_creds')) || { email: 'admin@alasli.com', pass: 'Mo88886#h' };    
        let selectedImagesBase64 = [];    
        let generatedOtp = null;  
        let forgotTargetEmail = null;  
        let currentLang = localStorage.getItem('alasli_lang') || 'ar';
    
        function init() {    
            applyLanguage();
            if(currentUser) {     
                document.getElementById('loginBtn').classList.add('hidden');     
                document.getElementById('userMenu').classList.remove('hidden');     
                document.getElementById('userMenu').classList.add('flex');     
                document.getElementById('userNameDisplay').innerText = currentUser.name;  
                updateWalletDisplay();     
            }    
            renderProducts('الكل');    
        }    
        window.onload = init;    

        function toggleLanguage() {
            currentLang = currentLang === 'ar' ? 'en' : 'ar';
            localStorage.setItem('alasli_lang', currentLang);
            applyLanguage();
        }

        function applyLanguage() {
            document.documentElement.lang = currentLang;
            document.documentElement.dir = currentLang === 'ar' ? 'rtl' : 'ltr';
            document.getElementById('langToggleBtn').innerText = currentLang === 'ar' ? 'EN' : 'عربي';

            document.querySelectorAll('[data-ar]').forEach(el => {
                if(el.getAttribute(`data-${currentLang}`)) { el.innerHTML = el.getAttribute(`data-${currentLang}`); }
            });
            document.querySelectorAll('[data-placeholder-ar]').forEach(el => {
                if(el.getAttribute(`data-placeholder-${currentLang}`)) { el.placeholder = el.getAttribute(`data-placeholder-${currentLang}`); }
            });

            renderProducts(currentFilter);
            updateCartDisplay();
            updateWalletDisplay();
            if(currentUser) renderMyOrders();
        }
    
        function openModal(id) { document.getElementById(id).classList.add('active'); }    
        function closeModal(id) { document.getElementById(id).classList.remove('active'); }    
            
        function updateCities() {    
            const gov = document.getElementById('checkoutGov').value;     
            const citySelect = document.getElementById('checkoutCity');     
            citySelect.innerHTML = `<option value="">${currentLang === 'ar' ? 'المركز/المدينة' : 'City'}</option>`;    
            if(gov && egyptData[gov]) {     
                egyptData[gov].forEach(city => { citySelect.innerHTML += `<option value="${city}">${city}</option>`; });     
            }    
        }    

        function showRegisterView() {
            document.getElementById('authModalTitle').innerText = currentLang === 'ar' ? "إنشاء حساب جديد" : "Create Account";
            document.getElementById('loginFormSection').classList.add('hidden');
            document.getElementById('forgotFormSection').classList.add('hidden');
            document.getElementById('registerFormSection').classList.remove('hidden');
        }

        function showForgotView() {
            document.getElementById('authModalTitle').innerText = currentLang === 'ar' ? "استعادة كلمة المرور" : "Reset Password";
            document.getElementById('loginFormSection').classList.add('hidden');
            document.getElementById('registerFormSection').classList.add('hidden');
            document.getElementById('forgotFormSection').classList.remove('hidden');
            document.getElementById('forgotStep1').classList.remove('hidden');
            document.getElementById('forgotStep2').classList.add('hidden');
        }

        function showLoginView() {
            document.getElementById('authModalTitle').innerText = currentLang === 'ar' ? "تسجيل الدخول" : "Login";
            document.getElementById('registerFormSection').classList.add('hidden');
            document.getElementById('forgotFormSection').classList.add('hidden');
            document.getElementById('loginFormSection').classList.remove('hidden');
        }

        function handleUserRegister() {
            const name = document.getElementById('regName').value.trim();
            const email = document.getElementById('regEmail').value.trim().toLowerCase();
            const password = document.getElementById('regPassword').value;

            if(!name || !email || !password) return alert(i18n[currentLang].fillFields);
            if(!email.includes('@')) return alert(i18n[currentLang].invalidEmail);
            
            let usersData = JSON.parse(localStorage.getItem('alasli_users')) || {};
            if(usersData[email]) return alert(i18n[currentLang].emailExists);

            usersData[email] = { name, email, password, walletBalance: 0 };
            localStorage.setItem('alasli_users', JSON.stringify(usersData));

            alert(i18n[currentLang].accCreated);
            login(email, name);
        }

        function handleUserLogin() {
            const email = document.getElementById('authEmail').value.trim().toLowerCase();
            const password = document.getElementById('authPassword').value;

            if(!email || !password) return alert(i18n[currentLang].enterCredentials);

            let usersData = JSON.parse(localStorage.getItem('alasli_users')) || {};
            if(!usersData[email]) return alert(i18n[currentLang].notRegistered);
            if(usersData[email].password && usersData[email].password !== password) return alert(i18n[currentLang].wrongPass);

            login(email, usersData[email].name);
        }

        function sendOtpCode() {
            const email = document.getElementById('forgotEmail').value.trim().toLowerCase();
            if(!email) return alert(i18n[currentLang].enterEmailFirst);

            let usersData = JSON.parse(localStorage.getItem('alasli_users')) || {};
            if(!usersData[email]) return alert(i18n[currentLang].emailNotStore);

            forgotTargetEmail = email;
            generatedOtp = Math.floor(1000 + Math.random() * 9000);
            
            alert(`${i18n[currentLang].otpSent} ${generatedOtp}`);
            
            document.getElementById('forgotStep1').classList.add('hidden');
            document.getElementById('forgotStep2').classList.remove('hidden');
        }

        function verifyAndResetPassword() {
            const enteredOtp = document.getElementById('otpInput').value.trim();
            const newPass = document.getElementById('newPasswordInput').value;

            if(enteredOtp != generatedOtp) return alert(i18n[currentLang].wrongOtp);
            if(!newPass || newPass.length < 4) return alert(i18n[currentLang].shortPass);

            let usersData = JSON.parse(localStorage.getItem('alasli_users')) || {};
            if(usersData[forgotTargetEmail]) {
                usersData[forgotTargetEmail].password = newPass;
            }
            localStorage.setItem('alasli_users', JSON.stringify(usersData));

            alert(i18n[currentLang].passChanged);
            showLoginView();
        }
  
        function login(email, name) {    
            currentUser = { email, name };     
            localStorage.setItem('alasli_currentUser', JSON.stringify(currentUser));    
            let usersData = JSON.parse(localStorage.getItem('alasli_users')) || {};
            if(!usersData[email]) {     
                usersData[email] = { name, email, walletBalance: 0 };     
                localStorage.setItem('alasli_users', JSON.stringify(usersData));     
            }    
            closeModal('loginModal'); init();    
        }    
  
        function logout() {     
            localStorage.removeItem('alasli_currentUser'); currentUser = null; cart = [];     
            document.getElementById('loginBtn').classList.remove('hidden');     
            document.getElementById('userMenu').classList.add('hidden');     
            document.getElementById('userMenu').classList.remove('flex');     
            updateCartDisplay();    
            location.reload();  
        }    
  
        function updateWalletDisplay() {     
            if(!currentUser) return;     
            let usersData = JSON.parse(localStorage.getItem('alasli_users')) || {};     
            const balance = usersData[currentUser.email]?.walletBalance || 0;     
            document.getElementById('walletBalanceDisplay').innerText = balance;     
            document.getElementById('modalWalletBalance').innerHTML = balance + ` <span class="text-sm">${i18n[currentLang].egp}</span>`;     
        }    
    
        function filterProducts(cat) { currentFilter = cat; renderProducts(cat); }    
        function renderProducts(category = currentFilter) {    
            products = JSON.parse(localStorage.getItem('alasli_products')) || [];     
            const grid = document.getElementById('productsGrid'); grid.innerHTML = '';    
                
            if(products.length === 0) {     
                grid.innerHTML = `<div class="col-span-2 md:col-span-4 text-center text-gray-500 py-16 bg-black/40 rounded-2xl border border-gray-800"><i class="fa-solid fa-box-open text-4xl mb-3 opacity-50 block text-gold"></i> ${i18n[currentLang].emptyProducts}</div>`; return;     
            }    
            products.forEach(p => {    
                if(category !== 'الكل' && p.category !== category) return;    
                const mainImg = p.images && p.images.length > 0 ? p.images[0] : 'https://via.placeholder.com/150';    
                const desc = p.desc ? `<p class="text-xs text-gray-400 mb-2 line-clamp-2" title="${p.desc}">${p.desc}</p>` : '';    
                const displayCat = currentLang === 'en' && catMap[p.category] ? catMap[p.category] : p.category;
                
                grid.innerHTML += `    
                    <div class="bg-gray-900 p-3 md:p-4 rounded-2xl shadow-lg border border-gray-800 hover:border-gold transition duration-300 group flex flex-col">    
                        <div class="relative overflow-hidden rounded-xl mb-3 border border-gray-800">    
                            <img src="${mainImg}" class="w-full h-40 md:h-56 object-cover cursor-pointer group-hover:scale-105 transition duration-500" onclick='openLightbox(${JSON.stringify(p.images)})'>    
                            <div class="absolute top-2 right-2 bg-black/70 backdrop-blur-sm text-gold text-xs px-2 py-1 rounded border border-gold/50">${displayCat}</div>    
                        </div>    
                        <h3 class="font-bold text-sm md:text-base text-gray-100 mb-1 truncate" title="${p.name}">${p.name}</h3>${desc}    
                        <div class="mt-auto flex justify-between items-end border-t border-gray-800 pt-3">    
                            <span class="font-black text-white text-lg" dir="ltr">${p.price} <span class="text-xs text-gray-400">${i18n[currentLang].egp}</span></span>    
                            <button onclick="addToCart('${p.id}')" class="bg-gold text-black w-10 h-10 rounded-full flex items-center justify-center hover:bg-yellow-600 shadow-lg transition hover:scale-110"><i class="fa-solid fa-cart-plus"></i></button>    
                        </div>    
                    </div>`;    
            });    
        }    
            
        function openLightbox(imgs) { if(!imgs || !imgs.length) return; currentLightboxImages = imgs; currentLightboxIndex = 0; updateLightbox(); openModal('lightboxModal'); }    
        function updateLightbox() { document.getElementById('lightboxImage').src = currentLightboxImages[currentLightboxIndex]; document.getElementById('lightboxDots').innerHTML = currentLightboxImages.map((_, i) => `<span class="w-2 h-2 rounded-full transition-all ${i === currentLightboxIndex ? 'bg-gold w-6' : 'bg-gray-600'}"></span>`).join(''); }    
        function changeLightboxImage(dir) { currentLightboxIndex += dir; if(currentLightboxIndex < 0) currentLightboxIndex = currentLightboxImages.length - 1; if(currentLightboxIndex >= currentLightboxImages.length) currentLightboxIndex = 0; updateLightbox(); }    
    
        function addToCart(id) {    
            if(!currentUser) return openModal('loginModal');     
            const existingItem = cart.find(p => p.id === id);    
            if(existingItem) {    
                existingItem.quantity += 1;    
            } else {    
                const product = products.find(p => p.id === id);    
                cart.push({...product, quantity: 1});    
            }    
            updateCartDisplay();    
            const cartIcon = document.getElementById('cartCount'); cartIcon.classList.add('scale-150', 'bg-gold', 'text-black'); setTimeout(() => cartIcon.classList.remove('scale-150', 'bg-gold', 'text-black'), 300);    
        }    
    
        function changeQty(index, delta) {    
            cart[index].quantity += delta;    
            if(cart[index].quantity <= 0) { cart.splice(index, 1); }    
            updateCartDisplay();    
        }    
    
        function updateCartDisplay() {    
            const totalQty = cart.reduce((sum, p) => sum + p.quantity, 0);    
            document.getElementById('cartCount').innerText = totalQty;     
            const items = document.getElementById('cartItems'); let total = 0; items.innerHTML = '';    
                
            if(cart.length === 0) { items.innerHTML = `<div class="text-center text-gray-500 py-8 text-sm bg-black/40 rounded-xl border border-gray-800">${i18n[currentLang].cartEmpty}</div>`; }    
                
            cart.forEach((p, i) => {    
                const itemTotal = parseFloat(p.price) * p.quantity;    
                total += itemTotal;    
                items.innerHTML += `    
                    <div class="flex justify-between items-center bg-black/60 border border-gray-800 p-3 rounded-xl text-sm gap-2">    
                        <div class="flex items-center gap-2 w-2/5">    
                            <img src="${p.images[0]}" class="w-10 h-10 object-cover rounded-lg border border-gray-700">    
                            <span class="truncate font-bold text-gray-200">${p.name}</span>    
                        </div>    
                        <div class="flex items-center bg-gray-900 rounded border border-gray-700" dir="ltr">    
                            <button onclick="changeQty(${i}, -1)" class="w-6 h-6 text-gold hover:bg-gray-800 rounded font-bold">-</button>    
                            <span class="w-5 text-center text-white text-xs">${p.quantity}</span>    
                            <button onclick="changeQty(${i}, 1)" class="w-6 h-6 text-gold hover:bg-gray-800 rounded font-bold">+</button>    
                        </div>    
                        <div class="font-bold text-gold flex items-center gap-2 text-xs" dir="ltr">    
                            <span class="whitespace-nowrap">${itemTotal} ${i18n[currentLang].egp}</span>    
                            <button onclick="cart.splice(${i},1); updateCartDisplay()" class="text-red-500 bg-red-900/30 w-7 h-7 rounded hover:bg-red-600 hover:text-white transition"><i class="fa-solid fa-trash text-xs"></i></button>    
                        </div>    
                    </div>`;    
            });    
            document.getElementById('cartTotal').innerText = total;    
        }    
    
        // ================= الدالة المحدثة والخالية من الأخطاء تماماً ================= //
        function checkout() {    
            try {
                if(!currentUser) { openModal('loginModal'); return; }
                if(!cart.length) { alert(i18n[currentLang].cartEmpty); return; }
                
                const gov = document.getElementById('checkoutGov').value;
                const city = document.getElementById('checkoutCity').value;
                const street = document.getElementById('checkoutAddress').value.trim();
                const phone = document.getElementById('checkoutPhone').value.trim();    
                
                if(!gov || !city || !street || !phone) { 
                    alert(i18n[currentLang].enterAddress); 
                    return; 
                }
                const fullAddress = `${gov} - ${city} - ${street}`;    
                    
                let total = cart.reduce((sum, p) => sum + (parseFloat(p.price) * p.quantity), 0);     
                
                let usersData = JSON.parse(localStorage.getItem('alasli_users')) || {};
                
                if(!usersData[currentUser.email]) {
                    usersData[currentUser.email] = { name: currentUser.name, email: currentUser.email, walletBalance: 0 };
                }

                if(usersData[currentUser.email].walletBalance < total) { 
                    alert(i18n[currentLang].noBalance); 
                    closeModal('cartModal'); 
                    openModal('walletModal'); 
                    return; 
                }    
                    
                // 1. خصم الرصيد
                usersData[currentUser.email].walletBalance -= total; 
                localStorage.setItem('alasli_users', JSON.stringify(usersData));    
                
                // 2. ضغط السلة وتخفيف المساحة عشان الآيفون ما يعلقش (بناخد صورة واحدة بس لكل منتج)
                const optimizedCart = cart.map(item => ({
                    id: item.id,
                    name: item.name,
                    price: item.price,
                    quantity: item.quantity,
                    images: [item.images[0]] // صورة واحدة كافية
                }));

                // 3. تسجيل الطلب
                const orderId = '#ORD-' + Math.floor(100000 + Math.random()*900000); 
                let ordersData = JSON.parse(localStorage.getItem('alasli_orders')) || [];    
                ordersData.push({ 
                    orderId, 
                    userId: currentUser.email, 
                    userName: currentUser.name, 
                    userPhone: phone, 
                    userAddress: fullAddress, 
                    date: new Date().toLocaleDateString(), 
                    items: optimizedCart, 
                    total 
                });    
                localStorage.setItem('alasli_orders', JSON.stringify(ordersData));    
                
                // 4. تنظيف السلة
                cart = []; 
                updateCartDisplay(); 
                updateWalletDisplay(); 
                closeModal('cartModal');    
                
                // 5. عرض رسالة النجاح
                const successOrderIdEl = document.getElementById('successOrderId');
                const successOrderTotalEl = document.getElementById('successOrderTotal');
                
                if (successOrderIdEl && successOrderTotalEl) {
                    successOrderIdEl.innerText = orderId;
                    successOrderTotalEl.innerText = total;
                    openModal('successModal');
                } else {
                    alert(i18n[currentLang].orderSuccess);
                }
                
                renderMyOrders();    

            } catch (error) {
                console.error("Checkout Error:", error);
                alert(i18n[currentLang].checkoutError + "\nتفاصيل: " + error.message);
            }
        }    
    
        function submitWalletRequest() {    
            if(!currentUser) return; const phone = document.getElementById('walletPhone').value, amount = document.getElementById('walletAmount').value;    
            if(!phone || !amount) return alert(i18n[currentLang].fillTransfer);    
            let requestsData = JSON.parse(localStorage.getItem('alasli_wallet_requests')) || [];    
            requestsData.push({ id: Date.now(), userId: currentUser.email, userName: currentUser.name, phone, amount: parseFloat(amount), date: new Date().toLocaleDateString(), status: 'قيد المراجعة' });    
            localStorage.setItem('alasli_wallet_requests', JSON.stringify(requestsData));    
            alert(i18n[currentLang].transferSent); closeModal('walletModal');    
        }    
    
        function renderMyOrders() {    
            if(!currentUser) return; 
            let ordersData = JSON.parse(localStorage.getItem('alasli_orders')) || []; 
            const list = document.getElementById('myOrdersList'); 
            const myOrders = ordersData.filter(o => o.userId === currentUser.email);    
            
            if(!myOrders.length) { list.innerHTML = `<div class="text-center text-gray-500 py-8 text-sm bg-black/40 rounded-xl border border-gray-800">${i18n[currentLang].emptyProducts}</div>`; return; }    
            list.innerHTML = myOrders.reverse().map(o => `    
                <div class="border border-gray-700 p-4 rounded-xl bg-black/60 text-sm shadow-sm relative overflow-hidden"><div class="absolute left-0 top-0 bottom-0 w-1 bg-gold"></div><div class="flex justify-between items-center font-bold border-b border-gray-700 pb-3 mb-3"><span class="text-black bg-gold px-2 py-1 rounded text-xs">${o.orderId}</span> <span class="text-white text-lg" dir="ltr">${o.total} <span class="text-xs">${i18n[currentLang].egp}</span></span></div>    
                <div class="text-xs text-gray-400 mb-4 flex justify-between"><span><i class="fa-regular fa-calendar text-gold mr-1"></i> ${o.date}</span><span><i class="fa-solid fa-box text-gold mr-1"></i> ${o.items.reduce((s, i) => s + (i.quantity||1), 0)} ${i18n[currentLang].pcs}</span></div>    
                <button onclick="navigator.clipboard.writeText('${o.orderId}'); alert(i18n[currentLang].copied)" class="bg-gray-800 border border-gray-700 hover:border-gold hover:text-white px-3 py-2 rounded-lg text-xs font-bold text-gray-400 w-full transition">${currentLang === 'ar' ? 'نسخ كود الطلب' : 'Copy Order Code'}</button></div>`).join('');    
        }    
        document.querySelector('button[onclick="openModal(\'ordersModal\')"]').addEventListener('click', renderMyOrders);    
    
        function sendChatMessage() {    
            const input = document.getElementById('chatInput'); if(!input.value.trim()) return;    
            document.getElementById('chatMessages').innerHTML += `<div class="bg-gold text-black p-3 rounded-xl rounded-tl-none self-end ml-auto mb-2 max-w-[85%] font-bold">${input.value}</div>`; input.value = '';    
            setTimeout(() => { document.getElementById('chatMessages').innerHTML += `<div class="bg-gray-800 border border-gray-700 text-gray-200 p-3 rounded-xl rounded-tr-none self-start mb-2 max-w-[85%]">${currentLang === 'ar' ? 'الدعم الفني سيتابع معك.' : 'Support will follow up with you.'}</div>`; }, 1000);    
        }    
    
        // الإدارة
        let pressTimer; const secretFooter = document.getElementById('secretFooter');    
        secretFooter.addEventListener('contextmenu', e => e.preventDefault());    
        secretFooter.addEventListener('touchstart', startPress, {passive: false}); secretFooter.addEventListener('touchend', cancelPress);    
        secretFooter.addEventListener('mousedown', startPress); secretFooter.addEventListener('mouseup', cancelPress); secretFooter.addEventListener('mouseleave', cancelPress);    
            
        function startPress(e) { pressTimer = setTimeout(() => { document.getElementById('adminLoginScreen').classList.remove('hidden'); document.getElementById('adminLoginScreen').classList.add('flex'); document.getElementById('adminEmail').value = adminCreds.email; }, 3000); }    
        function cancelPress() { clearTimeout(pressTimer); }    
        function closeAdminLogin() { document.getElementById('adminLoginScreen').classList.add('hidden'); document.getElementById('adminLoginScreen').classList.remove('flex'); document.getElementById('adminPassword').value = ''; }    
    
        function loginAdmin() {    
            if(document.getElementById('adminEmail').value === adminCreds.email && document.getElementById('adminPassword').value === adminCreds.pass) {    
                document.getElementById('adminLoginScreen').classList.add('hidden'); document.getElementById('customerView').classList.add('hidden');    
                document.getElementById('adminDashboard').classList.remove('hidden'); document.getElementById('adminDashboard').classList.add('flex');    
                document.getElementById('newAdminEmail').value = adminCreds.email; renderAdminData();    
            } else { alert('البيانات غير صحيحة!'); }    
        }    
        function exitAdmin() { document.getElementById('adminDashboard').classList.add('hidden'); document.getElementById('adminDashboard').classList.remove('flex'); document.getElementById('customerView').classList.remove('hidden'); document.getElementById('customerView').classList.add('flex'); document.getElementById('adminPassword').value = ''; renderProducts(currentFilter); }    
        function switchTab(tab) { document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active')); document.getElementById('tab-' + tab).classList.add('active'); }    
        function renderAdminData() { renderAdminProducts(); renderAdminOrders(); renderAdminWallet(); }    
    
        function calcPrice() { let cost = parseFloat(document.getElementById('pCost').value) || 0; let margin = parseFloat(document.getElementById('pMargin').value) || 0; document.getElementById('pFinalPrice').innerText = Math.ceil(cost + (cost * (margin / 100))); }    
        function previewImages() {    
            const files = document.getElementById('pImages').files; if(files.length > 5) return alert('الحد الأقصى 5 صور');    
            const preview = document.getElementById('imagePreviews'); preview.innerHTML = ''; selectedImagesBase64 = [];    
            Array.from(files).forEach(file => { const reader = new FileReader(); reader.onload = e => { selectedImagesBase64.push(e.target.result); preview.innerHTML += `<img src="${e.target.result}" class="w-16 h-16 object-cover rounded-lg border border-gold">`; }; reader.readAsDataURL(file); });    
        }    
            
        function addProduct() {    
            const name = document.getElementById('pName').value, desc = document.getElementById('pDesc').value, price = document.getElementById('pFinalPrice').innerText;    
            if(!name || selectedImagesBase64.length === 0 || price === "0") return alert('الرجاء إدخال البيانات المطلوبة');    
            products.push({ id: 'P' + Date.now(), name: name, desc: desc, category: document.getElementById('pCategory').value, price: price, images: selectedImagesBase64 });    
            localStorage.setItem('alasli_products', JSON.stringify(products));    
                
            document.getElementById('pName').value = ''; document.getElementById('pDesc').value = ''; document.getElementById('pCost').value = ''; document.getElementById('pImages').value = ''; document.getElementById('imagePreviews').innerHTML = ''; selectedImagesBase64 = []; calcPrice();    
                
            renderAdminProducts(); renderProducts(currentFilter); alert('تم النشر.');     
        }    
    
        function deleteProduct(productId) {    
            if(confirm('هل أنت متأكد من حذف هذا المنتج نهائياً من المتجر؟')) {    
                products = products.filter(p => p.id !== productId);    
                localStorage.setItem('alasli_products', JSON.stringify(products));    
                renderAdminProducts();     
                renderProducts(currentFilter);    
            }    
        }    
    
        function renderAdminProducts() {    
            const list = document.getElementById('adminProductsList'); if(products.length === 0) return list.innerHTML = '<div class="text-gray-500">لا توجد منتجات.</div>';    
            list.innerHTML = products.map(p => `    
                <div class="bg-gray-800 p-3 rounded-xl border border-gray-700 text-sm shadow">    
                    <img src="${p.images[0]}" class="w-full h-28 object-cover mb-3 rounded-lg border border-gray-700">    
                    <div class="font-bold truncate text-white">${p.name}</div>    
                    <div class="text-white font-black mb-3">${p.price} ج.م</div>    
                    <button onclick="deleteProduct('${p.id}')" class="text-xs bg-red-900/40 text-white w-full border border-red-800 rounded-lg py-2 hover:bg-red-600 transition">حذف</button>    
                </div>`).join('');    
        }    
    
        function renderAdminOrders() {    
            let ordersData = JSON.parse(localStorage.getItem('alasli_orders')) || [];
            const q = document.getElementById('orderSearch').value.toLowerCase(); const filteredOrders = ordersData.filter(o => o.orderId.toLowerCase().includes(q)).reverse();    
            const list = document.getElementById('adminOrdersList'); if(filteredOrders.length === 0) return list.innerHTML = '<div class="text-gray-500">لا توجد طلبات.</div>';    
            list.innerHTML = filteredOrders.map(o => `    
                <div class="bg-gray-800 p-5 rounded-2xl shadow-lg border-r-4 border-gold border-gray-700 text-sm relative">    
                    <div class="flex justify-between border-b border-gray-700 pb-3 mb-3"><span class="font-black text-black bg-gold px-3 py-1 rounded-lg">${o.orderId}</span><span class="font-black text-white text-lg bg-green-900/40 px-3 py-1 rounded-lg border border-green-800">${o.total} ج.م</span></div>    
                    <div class="mb-2 text-white"><i class="fa-solid fa-user text-gray-500 w-5"></i> ${o.userName} <span class="text-xs text-gray-500">(${o.userId})</span></div>    
                    <div class="mb-2 text-white"><i class="fa-solid fa-phone text-gray-500 w-5"></i> <span class="text-gold tracking-widest">${o.userPhone}</span></div>    
                    <div class="mb-4 text-gray-300"><i class="fa-solid fa-map-location-dot text-gray-500 w-5"></i> ${o.userAddress}</div>    
                    <div class="text-sm bg-black p-4 rounded-xl border border-gray-700"><strong class="text-gold block mb-3 border-b border-gray-800 pb-2">المنتجات المطلوبة والكميات:</strong>    
                        <div class="flex flex-col gap-3">${o.items.map(i => `    
                            <div class="flex items-center gap-3 bg-gray-800 p-2 rounded-lg border border-gray-700">    
                                <img src="${i.images[0]}" class="w-12 h-12 rounded object-cover border border-gold">    
                                <div class="flex-1">    
                                    <div class="font-bold text-white text-xs">${i.name}</div>    
                                    <div class="text-gold font-bold text-xs mt-1">${i.price} ج.م <span class="text-gray-400 font-normal ml-1">× ${i.quantity || 1} قطع</span> = <span class="text-white">${parseFloat(i.price) * (i.quantity || 1)} ج.م</span></div>    
                                </div>    
                            </div>`).join('')}</div>    
                    </div><div class="text-xs text-gray-500 mt-4">${o.date}</div></div>`).join('');    
        }    
            
        function renderAdminWallet() {    
            let requestsData = JSON.parse(localStorage.getItem('alasli_wallet_requests')) || [];
            const pending = requestsData.filter(r => r.status === 'قيد المراجعة'); const list = document.getElementById('adminWalletList');    
            if(pending.length === 0) return list.innerHTML = '<div class="text-gray-500 p-8 text-center bg-gray-800/50 rounded-xl">لا توجد طلبات شحن.</div>';    
            list.innerHTML = pending.map(r => `    
                <div class="bg-gray-800 p-5 rounded-2xl shadow-lg flex flex-col md:flex-row justify-between items-start md:items-center text-sm border-r-4 border-red-600 border-gray-700 gap-5">    
                    <div class="flex-1">    
                        <div class="font-bold text-white text-lg mb-1">${r.userName}</div><div class="text-gray-500 text-xs mb-3">${r.userId}</div>    
                        <div class="bg-black/60 p-3 rounded-lg border border-gray-700 inline-block"><div class="text-gray-400 text-xs">رقم المحول:</div><div class="font-black text-white text-lg tracking-widest">${r.phone}</div></div>    
                        <div class="inline-block ml-4"><div class="text-gray-400 text-xs">المبلغ:</div><div class="text-2xl font-black text-green-500">${r.amount} <span class="text-sm">ج.م</span></div></div>    
                    </div>    
                    <div class="flex gap-3 w-full md:w-auto"><button onclick="handleWallet(${r.id}, true)" class="flex-1 md:flex-none bg-green-600 text-white px-5 py-3 rounded-lg font-bold">قبول</button><button onclick="handleWallet(${r.id}, false)" class="flex-1 md:flex-none bg-red-600 text-white px-5 py-3 rounded-lg font-bold">رفض</button></div>    
                </div>`).join('');    
        }    
            
        function handleWallet(id, isApproved) {    
            let requestsData = JSON.parse(localStorage.getItem('alasli_wallet_requests')) || [];
            let usersData = JSON.parse(localStorage.getItem('alasli_users')) || {};
            const idx = requestsData.findIndex(r => r.id === id);    
            if(idx > -1) {    
                if(isApproved && usersData[requestsData[idx].userId]) {    
                    usersData[requestsData[idx].userId].walletBalance += parseFloat(requestsData[idx].amount); 
                    localStorage.setItem('alasli_users', JSON.stringify(usersData));    
                    if(currentUser && currentUser.email === requestsData[idx].userId) { updateWalletDisplay(); }    
                }    
                requestsData[idx].status = isApproved ? 'مقبول' : 'مرفوض'; localStorage.setItem('alasli_wallet_requests', JSON.stringify(requestsData)); renderAdminWallet();    
            }    
        }    
            
        function updateCredentials() {    
            const e = document.getElementById('newAdminEmail').value, p = document.getElementById('newAdminPassword').value;    
            if(e && p) { adminCreds = {email: e, pass: p}; localStorage.setItem('alasli_admin_creds', JSON.stringify(adminCreds)); alert('تم تحديث بيانات الدخول بنجاح!'); document.getElementById('newAdminPassword').value = ''; }    
        }    
    </script>    
</body>    
</html>

