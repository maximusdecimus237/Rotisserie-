<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ROTISSERIE — Operational Dashboard</title>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600;700&family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        :root {
            --bg-warm: #FAF8F5;
            --surface: #FFFFFF;
            --border-light: #EAE3D8;
            --primary: #9E2A2B;
            --primary-hover: #7A2021;
            --accent: #E65F2B;
            --accent-light: #FDF2EE;
            --text-main: #2B2523;
            --text-muted: #706661;
            --success: #2E7D32;
            --success-light: #E8F5E9;
            --warning: #EF6C00;
            --warning-light: #FFF3E0;
            
            --font-heading: 'Playfair Display', serif;
            --font-ui: 'Plus Jakarta Sans', sans-serif;
            --radius: 12px;
            --transition: all 0.2s ease;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: var(--font-ui);
            background-color: var(--bg-warm);
            color: var(--text-main);
            display: flex;
            min-height: 100vh;
        }

        /* --- SIDEBAR --- */
        aside {
            width: 260px;
            background: var(--surface);
            border-right: 1px solid var(--border-light);
            display: flex;
            flex-direction: column;
            position: fixed;
            height: 100vh;
            left: 0;
            top: 0;
            z-index: 100;
        }
        .sidebar-header {
            padding: 2rem 1.5rem;
            border-bottom: 1px solid var(--border-light);
        }
        .sidebar-brand {
            font-family: var(--font-heading);
            font-size: 1.6rem;
            color: var(--primary);
            font-weight: 700;
        }
        .sidebar-location {
            font-size: 0.75rem;
            color: var(--text-muted);
            margin-top: 0.25rem;
        }
        .nav-list {
            list-style: none;
            padding: 1.5rem 0.75rem;
            flex: 1;
        }
        .nav-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 0.85rem 1rem;
            color: var(--text-muted);
            font-weight: 500;
            border-radius: var(--radius);
            cursor: pointer;
            margin-bottom: 0.25rem;
            transition: var(--transition);
        }
        .nav-item:hover, .nav-item.active {
            background-color: var(--accent-light);
            color: var(--primary);
        }

        /* --- MAIN CONTENT --- */
        main {
            margin-left: 260px;
            flex: 1;
            padding: 2.5rem;
            max-width: 1400px;
        }
        header {
            margin-bottom: 2.5rem;
        }
        h2.page-title {
            font-family: var(--font-heading);
            font-size: 2.25rem;
            color: var(--text-main);
        }

        /* --- FORMS & INPUTS --- */
        .entry-box {
            background: var(--surface);
            border: 1px solid var(--border-light);
            border-radius: var(--radius);
            padding: 1.5rem;
            height: fit-content;
        }
        .entry-box h3 {
            font-family: var(--font-heading);
            margin-bottom: 1.25rem;
            color: var(--primary);
        }
        .form-group {
            margin-bottom: 1.25rem;
        }
        .form-group label {
            display: block;
            font-size: 0.85rem;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: var(--text-main);
        }
        .form-control {
            width: 100%;
            padding: 0.75rem 1rem;
            font-family: var(--font-ui);
            font-size: 0.9rem;
            border: 1px solid var(--border-light);
            border-radius: var(--radius);
            outline: none;
            background-color: var(--bg-warm);
        }
        .form-control:focus {
            border-color: var(--accent);
            background-color: var(--surface);
        }

        /* --- BUTTONS --- */
        .btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 0.85rem 1.25rem;
            font-family: var(--font-ui);
            font-weight: 600;
            border-radius: var(--radius);
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            width: 100%;
            transition: var(--transition);
        }
        .btn:hover {
            background-color: var(--primary-hover);
        }

        /* --- LAYOUT SPLIT --- */
        .data-split {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 2rem;
            align-items: start;
        }

        /* --- STAT CARDS --- */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2.5rem;
        }
        .stat-card {
            background: var(--surface);
            border: 1px solid var(--border-light);
            border-radius: var(--radius);
            padding: 1.5rem;
        }
        .stat-label {
            font-size: 0.85rem;
            color: var(--text-muted);
            text-transform: uppercase;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }
        .stat-value {
            font-family: var(--font-heading);
            font-size: 2rem;
            color: var(--text-main);
        }

        /* --- TABLES --- */
        .table-container {
            background: var(--surface);
            border: 1px solid var(--border-light);
            border-radius: var(--radius);
            overflow: hidden;
        }
        .table-header {
            padding: 1.25rem 1.5rem;
            border-bottom: 1px solid var(--border-light);
            background: #FFF;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
            font-size: 0.9rem;
        }
        th {
            background-color: var(--bg-warm);
            padding: 1rem 1.5rem;
            color: var(--text-muted);
            font-weight: 600;
            border-bottom: 1px solid var(--border-light);
        }
        td {
            padding: 1.25rem 1.5rem;
            border-bottom: 1px solid var(--border-light);
            color: var(--text-main);
        }
        tr:hover td {
            background-color: var(--bg-warm);
        }

        /* --- PILLS --- */
        .pill {
            display: inline-flex;
            padding: 0.25rem 0.75rem;
            border-radius: 50px;
            font-size: 0.75rem;
            font-weight: 600;
        }
        .pill-active { background-color: var(--success-light); color: var(--success); }
        .pill-pending { background-color: var(--warning-light); color: var(--warning); }

        /* --- VIEW CONTROLLER --- */
        .app-view { display: none; }
        .app-view.active-view { display: block; }
    </style>
</head>
<body>

    <!-- --- SIDEBAR NAVIGATION --- -->
    <aside>
        <div class="sidebar-header">
            <div class="sidebar-brand">ROTISSERIE</div>
            <div class="sidebar-location">College Tiniali, Golaghat</div>
        </div>
        <ul class="nav-list">
            <li class="nav-item active" onclick="switchView('dashboard', this)"><i data-lucide="layout-dashboard"></i>Dashboard</li>
            <li class="nav-item" onclick="switchView('orders', this)"><i data-lucide="utensils-crossedd"></i>Daily Orders</li>
            <li class="nav-item" onclick="switchView('inventory', this)"><i data-lucide="boxes"></i>Stock Inventory</li>
            <li class="nav-item" onclick="switchView('staff', this)"><i data-lucide="users"></i>Staff Registry</li>
            <li class="nav-item" onclick="switchView('customers', this)"><i data-lucide="heart-handshake"></i>Guest Ledger</li>
        </ul>
    </aside>

    <!-- --- MAIN CONTAINER --- -->
    <main>
        
        <!-- MODULE 1: DASHBOARD OVERVIEW -->
        <div id="view-dashboard" class="app-view active-view">
            <header>
                <h2 class="page-title">Live Kitchen Pulse</h2>
                <p style="color: var(--text-muted);">Real-time metrics calculated from entries</p>
            </header>

            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-label">Daily Sales / Profit</div>
                    <div class="stat-value" id="dash-profit">₹430</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Total Cash collected</div>
                    <div class="stat-value" id="dash-cash">₹430</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Total Tips Earned</div>
                    <div class="stat-value" id="dash-tips">₹50</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Avg Serving Time</div>
                    <div class="stat-value" id="dash-time">15 min</div>
                </div>
            </div>

            <div class="table-container">
                <div class="table-header"><h3>Active Running Orders Context</h3></div>
                <table id="dash-orders-table">
                    <thead>
                        <tr>
                            <th>Location</th>
                            <th>Item</th>
                            <th>Total Cost</th>
                            <th>Status</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Automatically syncs with Daily Orders -->
                    </tbody>
                </table>
            </div>
        </div>

        <!-- MODULE 2: DAILY ORDERS ENTRY -->
        <div id="view-orders" class="app-view">
            <header>
                <h2 class="page-title">Order Entry Register</h2>
                <p style="color: var(--text-muted);">Log chicken roasts, track service speed, and calculate cash drawers.</p>
            </header>
            
            <div class="data-split">
                <div class="entry-box">
                    <h3>New Order Ticket</h3>
                    <div class="form-group">
                        <label>Menu Selection</label>
                        <select class="form-control" id="ord-item">
                            <option value="Classic Half Roasted Chicken|240">Classic Half Roasted Chicken — ₹240</option>
                            <option value="Spiced Quarter Breast|140">Spiced Quarter Breast — ₹140</option>
                            <option value="Full Wood-Fired Banquet|450">Full Wood-Fired Banquet — ₹450</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Table No. / Channel</label>
                        <input type="text" class="form-control" id="ord-table" placeholder="e.g. Table 3">
                    </div>
                    <div class="form-group">
                        <label>Prep + Serving Time (Minutes)</label>
                        <input type="number" class="form-control" id="ord-time" placeholder="e.g. 15" value="15">
                    </div>
                    <div class="form-group">
                        <label>Tips Gratuity (₹)</label>
                        <input type="number" class="form-control" id="ord-tips" placeholder="0" value="20">
                    </div>
                    <button class="btn" type="button" onclick="submitOrder()">Save Order Ticket</button>
                </div>

                <div class="table-container">
                    <div class="table-header"><h3>Daily Transaction Logs</h3></div>
                    <table id="main-orders-list">
                        <thead>
                            <tr>
                                <th>Location</th>
                                <th>Item</th>
                                <th>Bill Price</th>
                                <th>Time Taken</th>
                                <th>Tips</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Table 2</td>
                                <td>Classic Half Roasted Chicken</td>
                                <td>₹240</td>
                                <td>15 mins</td>
                                <td>₹30</td>
                            </tr>
                            <tr>
                                <td>Quick Counter</td>
                                <td>Spiced Quarter Breast</td>
                                <td>₹140</td>
                                <td>12 mins</td>
                                <td>₹20</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- MODULE 3: INVENTORY ENTRY -->
        <div id="view-inventory" class="app-view">
            <header>
                <h2 class="page-title">Inventory & Stock Tracking</h2>
                <p style="color: var(--text-muted);">Add new supplies and keep raw items updated.</p>
            </header>

            <div class="data-split">
                <div class="entry-box">
                    <h3>Add Stock Item</h3>
                    <div class="form-group">
                        <label>Ingredient / Supply Item Name</label>
                        <input type="text" class="form-control" id="inv-name" placeholder="e.g. Fresh Broiler Chicken">
                    </div>
                    <div class="form-group">
                        <label>Current Stock Quantity</label>
                        <input type="text" class="form-control" id="inv-qty" placeholder="e.g. 50 Kgs">
                    </div>
                    <div class="form-group">
                        <label>Storage Room / Location</label>
                        <input type="text" class="form-control" id="inv-loc" placeholder="e.g. Deep Freezer 1">
                    </div>
                    <button class="btn" type="button" onclick="submitInventory()">Log Inventory Item</button>
                </div>

                <div class="table-container">
                    <div class="table-header"><h3>Current Kitchen Stock Levels</h3></div>
                    <table id="main-inventory-list">
                        <thead>
                            <tr>
                                <th>Item Name</th>
                                <th>Available Stock</th>
                                <th>Storage Location</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Fresh Whole Chickens</td>
                                <td>42 Kgs</td>
                                <td>Deep Freezer A</td>
                            </tr>
                            <tr>
                                <td>Assam Wood Fire Logs</td>
                                <td>12 Bundles</td>
                                <td>Dry Backyard Depot</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- MODULE 4: STAFF REGISTRY -->
        <div id="view-staff" class="app-view">
            <header>
                <h2 class="page-title">Staff Registry & Shifts</h2>
                <p style="color: var(--text-muted);">Manage workforce roles and team duty tracking.</p>
            </header>

            <div class="data-split">
                <div class="entry-box">
                    <h3>Add New Staff Member</h3>
                    <div class="form-group">
                        <label>Employee Name</label>
                        <input type="text" class="form-control" id="staff-name" placeholder="Full name">
                    </div>
                    <div class="form-group">
                        <label>Assigned Work Role</label>
                        <select class="form-control" id="staff-role">
                            <option value="Head Pitmaster Roaster">Head Pitmaster Roaster</option>
                            <option value="Line Cook / Prep Master">Line Cook / Prep Master</option>
                            <option value="Floor Steward / Waiter">Floor Steward / Waiter</option>
                            <option value="Cashier & Accountant">Cashier & Accountant</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Shift Timing Details</label>
                        <input type="text" class="form-control" id="staff-shift" placeholder="e.g. Morning (8 AM - 4 PM)">
                    </div>
                    <button class="btn" type="button" onclick="submitStaff()">Register Employee</button>
                </div>

                <div class="table-container">
                    <div class="table-header"><h3>Active Restaurant Team</h3></div>
                    <table id="main-staff-list">
                        <thead>
                            <tr>
                                <th>Employee Name</th>
                                <th>Role</th>
                                <th>Assigned Shift</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Jitendra Gogoi</td>
                                <td>Head Pitmaster Roaster</td>
                                <td>All-Day (11 AM - 10 PM)</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- MODULE 5: GUEST LEDGER & RATINGS -->
        <div id="view-customers" class="app-view">
            <header>
                <h2 class="page-title">Guest Ledger & Ratings</h2>
                <p style="color: var(--text-muted);">Keep details of regular customers and feedback.</p>
            </header>

            <div class="data-split">
                <div class="entry-box">
                    <h3>Log Guest Feedback</h3>
                    <div class="form-group">
                        <label>Customer Name / Table Identifier</label>
                        <input type="text" class="form-control" id="cust-name" placeholder="Guest Name or Phone">
                    </div>
                    <div class="form-group">
                        <label>Star Rating Given</label>
                        <select class="form-control" id="cust-rating">
                            <option value="⭐⭐⭐⭐⭐ 5.0 Stars">⭐⭐⭐⭐⭐ 5.0 Stars</option>
                            <option value="⭐⭐⭐⭐ 4.0 Stars">⭐⭐⭐⭐ 4.0 Stars</option>
                            <option value="⭐⭐⭐ 3.0 Stars">⭐⭐⭐ 3.0 Stars</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Notes / Preferences</label>
                        <input type="text" class="form-control" id="cust-note" placeholder="e.g. Prefers extra spicy glaze sauce">
                    </div>
                    <button class="btn" type="button" onclick="submitCustomer()">Save Guest Feedback</button>
                </div>

                <div class="table-container">
                    <div class="table-header"><h3>Guest Profile & Review Archive</h3></div>
                    <table id="main-customer-list">
                        <thead>
                            <tr>
                                <th>Guest Identity</th>
                                <th>Rating Score</th>
                                <th>Kitchen Notes</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Ananya B.</td>
                                <td>⭐⭐⭐⭐⭐ 5.0 Stars</td>
                                <td>Regular counter order. Prefers extra spice glaze.</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

    </main>

    <!-- --- DATA HANDLING LOGIC --- -->
    <script>
        // Initialize dynamic icons
        window.addEventListener('DOMContentLoaded', () => { 
            lucide.createIcons(); 
            recalculateDashboardTotals();
        });

        // Simple view switcher
        function switchView(viewId, clickedElement) {
            document.querySelectorAll('.app-view').forEach(view => view.classList.remove('active-view'));
            document.getElementById('view-' + viewId).classList.add('active-view');

            if(clickedElement) {
                document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
                clickedElement.classList.add('active');
            }
        }

        // Calculations & Table Sync Logic
        function recalculateDashboardTotals() {
            let totalCash = 0;
            let totalTips = 0;
            let combinedMinutes = 0;
            let orderRows = document.querySelectorAll('#main-orders-list tbody tr');
            
            let dashTableBody = document.querySelector('#dash-orders-table tbody');
            dashTableBody.innerHTML = ''; // Reset overview context

            orderRows.forEach(row => {
                let cells = row.getElementsByTagName('td');
                let loc = cells[0].innerText;
                let item = cells[1].innerText;
                let price = parseInt(cells[2].innerText.replace('₹', '')) || 0;
                let time = parseInt(cells[3].innerText.replace(' mins', '')) || 0;
                let tips = parseInt(cells[4].innerText.replace('₹', '')) || 0;

                totalCash += price;
                totalTips += tips;
                combinedMinutes += time;

                // Mirror to core dashboard display
                let quickRow = dashTableBody.insertRow();
                quickRow.innerHTML = `<td><b>${loc}</b></td><td>${item}</td><td>₹${price}</td><td><span class="pill pill-active">Served</span></td>`;
            });

            let avgTime = orderRows.length > 0 ? Math.round(combinedMinutes / orderRows.length) : 0;

            // Update UI elements
            document.getElementById('dash-profit').innerText = '₹' + totalCash;
            document.getElementById('dash-cash').innerText = '₹' + (totalCash + totalTips);
            document.getElementById('dash-tips').innerText = '₹' + totalTips;
            document.getElementById('dash-time').innerText = avgTime + ' min';
        }

        // Form 1: Add New Order
        function submitOrder() {
            const dropdown = document.getElementById('ord-item');
            const itemValue = dropdown.value.split('|');
            const itemName = itemValue[0];
            const itemPrice = itemValue[1];
            
            const tableNo = document.getElementById('ord-table').value.trim();
            const serviceTime = document.getElementById('ord-time').value.trim();
            const tipsAmount = document.getElementById('ord-tips').value.trim();

            if (!tableNo) { alert('Please enter a Table No. or Channel name.'); return; }

            const tableRef = document.getElementById('main-orders-list').getElementsByTagName('tbody')[0];
            const newRow = tableRef.insertRow(0); // Insert at top

            newRow.innerHTML = `
                <td>${tableNo}</td>
                <td>${itemName}</td>
                <td>₹${itemPrice}</td>
                <td>${serviceTime} mins</td>
                <td>₹${tipsAmount || 0}</td>
            `;

            // Reset Input Values safely
            document.getElementById('ord-table').value = '';
            
            recalculateDashboardTotals();
            alert('Order Ticket logged successfully!');
        }

        // Form 2: Add Inventory Asset
        function submitInventory() {
            const name = document.getElementById('inv-name').value.trim();
            const qty = document.getElementById('inv-qty').value.trim();
            const loc = document.getElementById('inv-loc').value.trim();

            if (!name || !qty) { alert('Please fill out the item name and quantity.'); return; }

            const tableRef = document.getElementById('main-inventory-list').getElementsByTagName('tbody')[0];
            const newRow = tableRef.insertRow(0);
            newRow.innerHTML = `<td><b>${name}</b></td><td>${qty}</td><td>${loc || 'Main Depot'}</td>`;

            document.getElementById('inv-name').value = '';
            document.getElementById('inv-qty').value = '';
            document.getElementById('inv-loc').value = '';
            alert('Inventory stock row added!');
        }

        // Form 3: Register Staff
        function submitStaff() {
            const name = document.getElementById('staff-name').value.trim();
            const role = document.getElementById('staff-role').value;
            const shift = document.getElementById('staff-shift').value.trim();

            if (!name || !shift) { alert('Please complete Name and Shift timings.'); return; }

            const tableRef = document.getElementById('main-staff-list').getElementsByTagName('tbody')[0];
            const newRow = tableRef.insertRow(0);
            newRow.innerHTML = `<td><b>${name}</b></td><td>${role}</td><td>${shift}</td>`;

            document.getElementById('staff-name').value = '';
            document.getElementById('staff-shift').value = '';
            alert('Staff member registered!');
        }

        // Form 4: Log Customer Feedback
        function submitCustomer() {
            const name = document.getElementById('cust-name').value.trim();
            const rating = document.getElementById('cust-rating').value;
            const note = document.getElementById('cust-note').value.trim();

            if (!name) { alert('Please identify the guest or target table.'); return; }

            const tableRef = document.getElementById('main-customer-list').getElementsByTagName('tbody')[0];
            const newRow = tableRef.insertRow(0);
            newRow.innerHTML = `<td><b>${name}</b></td><td>${rating}</td><td>${note || 'None'}</td>`;

            document.getElementById('cust-name').value = '';
            document.getElementById('cust-note').value = '';
            alert('Customer review file saved!');
        }
    </script>
</body>
</html>
