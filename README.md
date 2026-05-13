<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Event Bazar SMP IPEKA PLUIT</title>

<style>

body{
    font-family:Arial;
    margin:0;
    background:#fff5eb;
}

header{
    background:#ff7a00;
    color:white;
    padding:15px;
    text-align:center;
}

.logo{
    width:140px;
    height:140px;
    border-radius:50%;
    object-fit:cover;
    border:4px solid white;
    margin-bottom:10px;
}

nav{
    display:flex;
    justify-content:center;
    gap:10px;
    padding:10px;
    flex-wrap:wrap;
}

nav button{
    padding:10px 15px;
    border:none;
    border-radius:10px;
    background:#ff9d42;
    color:white;
    cursor:pointer;
}

.page{
    display:none;
    padding:20px;
}

.active{
    display:block;
}

.card{
    background:white;
    padding:20px;
    border-radius:15px;
    margin-top:15px;
    box-shadow:0 4px 10px rgba(0,0,0,0.1);
}

input, select{
    width:90%;
    padding:10px;
    margin-top:5px;
    margin-bottom:15px;
    border-radius:10px;
    border:1px solid #ccc;
}

.main-btn{
    width:100%;
    padding:12px;
    border:none;
    border-radius:10px;
    background:#ff7a00;
    color:white;
    font-size:16px;
    cursor:pointer;
}

.result{
    margin-top:15px;
    background:#fff0d9;
    padding:15px;
    border-radius:10px;
    line-height:1.8;
}

.food-list{
    display:flex;
    gap:15px;
    flex-wrap:wrap;
    justify-content:center;
}

.food-item{
    background:white;
    border-radius:15px;
    padding:15px;
    width:250px;
    box-shadow:0 4px 10px rgba(0,0,0,0.1);
    text-align:center;
}

.food-item img{
    width:100%;
    height:230px;
    object-fit:cover;
    border-radius:10px;
}

.food-item button{
    width:100%;
    padding:10px;
    border:none;
    border-radius:10px;
    background:#ff7a00;
    color:white;
    cursor:pointer;
}

.option-group{
    background:#fff5eb;
    padding:10px;
    border-radius:10px;
    margin-top:10px;
    text-align:left;
}

.option-group h4{
    color:#ff7a00;
}

.option-row{
    display:flex;
    align-items:center;
    gap:8px;
    margin-bottom:8px;
    font-size:14px;
}

.option-row input{
    width:auto;
    margin:0;
}

.cart-box{
    background:#fff0d9;
    padding:15px;
    border-radius:10px;
    margin-top:20px;
}

.cart-item{
    margin-bottom:10px;
}

.delete-btn{
    background:red;
    color:white;
    border:none;
    padding:5px 10px;
    border-radius:8px;
    cursor:pointer;
    margin-left:10px;
}

.qr-box{
    text-align:center;
    margin-top:20px;
}

.qr-box img{
    width:200px;
}

.seat-grid{
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(70px,1fr));
    gap:10px;
    margin-top:20px;
}

.seat-btn{
    padding:12px;
    border:none;
    border-radius:10px;
    background:#ffb067;
    cursor:pointer;
    font-weight:bold;
}

.seat-btn.selected{
    background:#ff7a00;
    color:white;
}

.seat-btn.booked{
    background:gray;
    color:white;
    cursor:not-allowed;
}

.admin-order{
    background:#fff0d9;
    padding:15px;
    border-radius:10px;
    margin-top:10px;
}

.search-box{
    width:95%;
}

</style>
</head>

<body>

<header>

<img src="https://imgur.com/HfP5KpF.png" class="logo">

<h1>Event Bazar SMP IPEKA PLUIT</h1>

</header>

<nav>
<button onclick="showPage('home')">Home</button>
<button onclick="showPage('ticket')">Booking Ticket</button>
<button onclick="showPage('seat')">Booking Seat</button>
<button onclick="showPage('food')">PO Makanan</button>
<button onclick="showPage('adminLogin')">Dashboard Admin</button>
</nav>

<!-- HOME -->
<div id="home" class="page active">

<div class="card">

<h2>Welcome</h2>

<p>Pesan tiket, seat, dan makanan digital.</p>

</div>

</div>

<!-- ADMIN LOGIN -->
<div id="adminLogin" class="page">

<div class="card">

<h2>Login Dashboard Admin</h2>

<input type="text" id="adminUsername" placeholder="Username">

<input type="password" id="adminPassword" placeholder="Password">

<button class="main-btn" onclick="loginAdmin()">
Login
</button>

<div id="loginResult" class="result"></div>

</div>

</div>

<!-- TICKET -->
<div id="ticket" class="page">

<div class="card">

<h2>Booking Ticket</h2>

<input type="text" id="ticketNama" placeholder="Nama">

<select id="ticketJenis">
<option value="25000">Regular - Rp25.000</option>
</select>

<input type="number" id="ticketJumlah" placeholder="Jumlah Ticket">

<button class="main-btn" onclick="bookingTicket()">
Pesan Ticket
</button>

<div id="ticketResult" class="result"></div>

</div>

</div>

<!-- SEAT -->
<div id="seat" class="page">

<div class="card">

<h2>Booking Seat</h2>

<input type="text" id="seatNama" placeholder="Nama">

<div class="seat-grid" id="seatGrid"></div>

<button class="main-btn" onclick="bookingSeat()">
Booking Seat
</button>

<div id="seatResult" class="result"></div>

</div>

</div>

<!-- FOOD -->
<div id="food" class="page">

<div class="card">

<h2>Pre-Order Makanan</h2>

<input type="text" id="foodNama" placeholder="Nama">

<div class="food-list">

<!-- MARTATO -->
<div class="food-item">

<img src="Martato.png">

<h3>Martato</h3>

<p>Rp17.000</p>

<input type="number" id="martatoJumlah" placeholder="Jumlah">

<div class="option-group">

<h4>Saus (Free)</h4>

<label class="option-row">
<input type="checkbox" class="martato-option" value="Tomat">
Tomat
</label>

<label class="option-row">
<input type="checkbox" class="martato-option" value="Cabe">
Cabe
</label>

<h4>Toppings</h4>

<label class="option-row">
<input type="checkbox" class="martato-option" value="BQQ">
BQQ (+1k)
</label>

<label class="option-row">
<input type="checkbox" class="martato-option" value="Keju">
Keju (+1k)
</label>

<h4>Add On</h4>

<label class="option-row">
<input type="checkbox" id="mozarellaAddOn">
Mozzarella (+3k)
</label>

</div>

<button onclick="tambahMartato()">
Tambah
</button>

</div>

<!-- CHIHOBAN -->
<div class="food-item">

<img src="chihoban2.png">

<h3>Chihoban</h3>

<p>Rp16.000</p>

<input type="number" id="chihobanJumlah" placeholder="Jumlah">

<div class="option-group">

<h4>Toppings (Free)</h4>

<label class="option-row">
<input type="checkbox" class="chihoban-option" value="Oreo Crumble">
Oreo Crumble
</label>

<label class="option-row">
<input type="checkbox" class="chihoban-option" value="Regal Crumble">
Regal Crumble
</label>

<h4>Add On</h4>

<label class="option-row">
<input type="checkbox" id="bobaAddOn">
Boba (+2k)
</label>

<label class="option-row">
<input type="checkbox" id="eskrimAddOn">
Es Krim (+3k)
</label>

</div>

<button onclick="tambahChihoban()">
Tambah
</button>

</div>

<!-- CINCAU -->
<div class="food-item">

<img src="cincau.png">

<h3>Cincau & Co</h3>

<p>Rp15.000</p>

<input type="number" id="cincauJumlah" placeholder="Jumlah">

<button onclick="tambahMenu('Cincau & Co',15000,'cincauJumlah')">
Tambah
</button>

</div>

</div>

<div class="cart-box">

<h3>Keranjang Pesanan</h3>

<div id="cartList"></div>

<h3>Total: Rp<span id="cartTotal">0</span></h3>

<button class="main-btn" onclick="orderFood()">
Pesan Semua
</button>

</div>

<div class="qr-box">

<h3>Scan QRIS</h3>

<img src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=DIGIFESTPAY">

</div>

<div id="foodResult" class="result"></div>

</div>

</div>

<!-- ADMIN -->
<div id="admin" class="page">

<div class="card">

<h2>Dashboard Admin</h2>

<p>Total Ticket: <span id="totalTicket">0</span></p>

<p>Total Seat: <span id="totalSeat">0</span></p>

<p>Total Food: <span id="totalFood">0</span></p>

<input
type="text"
id="searchOrder"
class="search-box"
placeholder="Cari nama..."
onkeyup="searchOrder()"
>

<h3>Pesanan Masuk</h3>

<div id="adminOrders"></div>

</div>

</div>

<script>

let totalTicket = 0;
let totalSeat = 0;
let totalFood = 0;

let cart = [];
let cartTotal = 0;

let orders = [];

const scriptURL =
"https://script.google.com/macros/s/AKfycbwbZ8RnOlYE3E48NCc280mxeWIvFROmbZkEVPi3JCbI_1HkGS5FrZJQxIEwsYaMJ5iZ/exec";

let selectedSeat = "";
let bookedSeats = [];

function showPage(pageId){

    let pages = document.querySelectorAll(".page");

    pages.forEach(page=>{
        page.classList.remove("active");
    });

    document.getElementById(pageId)
    .classList.add("active");
}

function loginAdmin(){

    let username =
    document.getElementById("adminUsername").value;

    let password =
    document.getElementById("adminPassword").value;

    if(username == "admin" && password == "nusarendang135"){

        showPage("admin");

    }else{

        document.getElementById("loginResult").innerHTML =
        "❌ Username atau Password salah";
    }
}

function bookingTicket(){

    let nama =
    document.getElementById("ticketNama").value;

    let jumlah =
    document.getElementById("ticketJumlah").value;

    document.getElementById("ticketResult").innerHTML =
    `
    ✅ Ticket berhasil dipesan<br><br>
    👤 Nama: ${nama}<br>
    🔢 Jumlah: ${jumlah}
    `;

    addAdminOrder("Ticket",nama,jumlah);
}

function createSeats(){

    let seatGrid =
    document.getElementById("seatGrid");

    for(let i=1;i<=160;i++){

        let seatCode = "A" + i;

        let btn =
        document.createElement("button");

        btn.innerText = seatCode;

        btn.classList.add("seat-btn");

        btn.onclick = function(){

            if(bookedSeats.includes(seatCode)){
                return;
            }

            document
            .querySelectorAll(".seat-btn")
            .forEach(seat=>{
                seat.classList.remove("selected");
            });

            btn.classList.add("selected");

            selectedSeat = seatCode;
        };

        seatGrid.appendChild(btn);
    }
}

createSeats();

function bookingSeat(){

    let nama =
    document.getElementById("seatNama").value;

    if(selectedSeat == ""){

        alert("Pilih seat dulu");

        return;
    }

    bookedSeats.push(selectedSeat);

    document
    .querySelectorAll(".seat-btn")
    .forEach(btn=>{

        if(btn.innerText == selectedSeat){

            btn.classList.remove("selected");

            btn.classList.add("booked");
        }
    });

    document.getElementById("seatResult").innerHTML =
    `
    ✅ Seat berhasil dibooking<br><br>
    👤 Nama: ${nama}<br>
    💺 Seat: ${selectedSeat}
    `;

    addAdminOrder(
        "Seat " + selectedSeat,
        nama,
        1
    );

    selectedSeat = "";
}

function tambahMartato(){

    let jumlah =
    Number(document.getElementById("martatoJumlah").value);

    if(jumlah <= 0){

        alert("Masukkan jumlah");

        return;
    }

    let harga = 17000;

    let pilihan = [];

    document
    .querySelectorAll(".martato-option")
    .forEach(option=>{

        if(option.checked){

            pilihan.push(option.value);

            if(option.value == "BQQ"){
                harga += 1000;
            }

            if(option.value == "Keju"){
                harga += 1000;
            }
        }
    });

    if(document.getElementById("mozarellaAddOn").checked){

        harga += 3000;

        pilihan.push("Mozzarella");
    }

    let total = harga * jumlah;

    cart.push({

        menu:"Martato (" + pilihan.join(", ") + ")",

        jumlah:jumlah,

        subtotal:total
    });

    cartTotal += total;

    updateCart();
}

function tambahChihoban(){

    let jumlah =
    Number(document.getElementById("chihobanJumlah").value);

    if(jumlah <= 0){

        alert("Masukkan jumlah");

        return;
    }

    let harga = 16000;

    let pilihan = [];

    document
    .querySelectorAll(".chihoban-option")
    .forEach(option=>{

        if(option.checked){

            pilihan.push(option.value);
        }
    });

    if(document.getElementById("bobaAddOn").checked){

        harga += 2000;

        pilihan.push("Boba");
    }

    if(document.getElementById("eskrimAddOn").checked){

        harga += 3000;

        pilihan.push("Es Krim");
    }

    let total = harga * jumlah;

    cart.push({

        menu:"Chihoban (" + pilihan.join(", ") + ")",

        jumlah:jumlah,

        subtotal:total
    });

    cartTotal += total;

    updateCart();
}

function tambahMenu(menu,harga,inputId){

    let jumlah =
    Number(document.getElementById(inputId).value);

    if(jumlah <= 0){

        alert("Masukkan jumlah");

        return;
    }

    let subtotal = harga * jumlah;

    cart.push({
        menu:menu,
        jumlah:jumlah,
        subtotal:subtotal
    });

    cartTotal += subtotal;

    updateCart();
}

function updateCart(){

    let cartList =
    document.getElementById("cartList");

    cartList.innerHTML = "";

    cart.forEach((item,index)=>{

        cartList.innerHTML +=
        `
        <div class="cart-item">

        ${item.menu}
        x ${item.jumlah}
        = Rp${item.subtotal}

        <button
        class="delete-btn"
        onclick="hapusMenu(${index})">

        Hapus

        </button>

        </div>
        `;
    });

    document.getElementById("cartTotal")
    .innerText = cartTotal;
}

function hapusMenu(index){

    cartTotal -= cart[index].subtotal;

    cart.splice(index,1);

    updateCart();
}

function orderFood(){

    let nama =
    document.getElementById("foodNama").value;

    if(cart.length == 0){

        alert("Keranjang kosong");

        return;
    }

    let hasil =
    `✅ Pesanan berhasil<br><br>👤 Nama: ${nama}<br><br>`;

    cart.forEach(item=>{

        hasil +=
        `
        🍴 ${item.menu}
        x ${item.jumlah}
        = Rp${item.subtotal}<br>
        `;

        addAdminOrder(
            item.menu,
            nama,
            item.jumlah
        );
    });

    hasil +=
    `
    <br>
    <b>Total: Rp${cartTotal}</b>
    `;

    document.getElementById("foodResult")
    .innerHTML = hasil;

    cart = [];
    cartTotal = 0;

    updateCart();
}

function addAdminOrder(menu,nama,jumlah){

    fetch(scriptURL,{

        method:"POST",

        body:JSON.stringify({

            nama:nama,
            menu:menu,
            jumlah:jumlah

        })
    });

    jumlah = Number(jumlah);

    if(menu == "Ticket"){

        totalTicket += jumlah;

        document.getElementById("totalTicket")
        .innerText = totalTicket;
    }

    if(menu.includes("Seat")){

        totalSeat += jumlah;

        document.getElementById("totalSeat")
        .innerText = totalSeat;
    }

    if(
        menu.includes("Martato")
        ||
        menu.includes("Chihoban")
        ||
        menu.includes("Cincau")
    ){

        totalFood += jumlah;

        document.getElementById("totalFood")
        .innerText = totalFood;
    }

    let existing =
    orders.find(order => order.nama === nama);

    if(existing){

        existing.items.push({
            menu:menu,
            jumlah:jumlah
        });

    }else{

        orders.push({

            nama:nama,

            items:[
                {
                    menu:menu,
                    jumlah:jumlah
                }
            ]
        });
    }

    renderOrders();
}

function renderOrders(){

    let adminOrders =
    document.getElementById("adminOrders");

    adminOrders.innerHTML = "";

    orders.forEach((order,index)=>{

        let itemsHTML = "";

        order.items.forEach(item=>{

            itemsHTML +=
            `
            ${item.menu}
            - ${item.jumlah}<br>
            `;
        });

        adminOrders.innerHTML +=
        `
        <div class="admin-order">

        <b>${order.nama}</b><br><br>

        ${itemsHTML}

        <button
        class="delete-btn"
        onclick="hapusOrder(${index})">

        Hapus Pesanan

        </button>

        </div>
        `;
    });
}

function hapusOrder(index){

    let konfirmasi =
    confirm("Hapus pesanan ini?");

    if(konfirmasi){

        let order = orders[index];

        fetch(scriptURL,{

            method:"POST",

            body:JSON.stringify({

                action:"delete",
                nama:order.nama

            })
        });

        orders.splice(index,1);

        renderOrders();
    }
}

function searchOrder(){

    let input =
    document.getElementById("searchOrder")
    .value
    .toLowerCase();

    let adminOrders =
    document.querySelectorAll(".admin-order");

    adminOrders.forEach(order=>{

        if(
            order.innerText
            .toLowerCase()
            .includes(input)
        ){

            order.style.display = "block";

        }else{

            order.style.display = "none";
        }
    });
}

</script>

</body>
</html>
