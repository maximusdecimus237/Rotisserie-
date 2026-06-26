<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ROTISSERIE — Restaurant Operations Dashboard</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,600;1,400&family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
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
            overflow-x: hidden;
        }

        /* --- LOGIN SCREEN OVERLAY --- */
        #login-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: var(--bg-warm);
            display: flex;
            z-index: 9999;
            transition: var(--transition);
        }
        .login-hero {
            flex: 1;
            background: linear-gradient(rgba(158, 42, 43, 0.4), rgba(43, 37, 35, 0.85)), url('https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&w=1200&q=80');
            background-size: cover;
            background-position: center;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            padding: 4rem;
            color: white;
        }
        .login-hero h1 {
            font-family: var(--font-heading);
            font-size: 3.5rem;
            margin-bottom: 1rem;
        }
        .login-form-container {
            width: 480px;
            background: var(--surface);
            padding: 4rem 3rem;
            display: flex;
            flex-direction: column;
            justify-content: center;
            border-left: 1px solid var(--border-light);
        }
        .login-brand {
            font-family: var(--font-heading);
            font-size: 2rem;
            color: var(--primary);
            margin-bottom: 0.5rem;
        }
        .login-subtitle {
            color: var(--text-muted);
            margin-bottom: 2.5rem;
            font-size: 0.95rem;
        }

        /* --- SIDEBAR NAVIGATION --- */
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
            font-size: 1.5rem;
            color: var(--primary);
            font-weight: 600;
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
            text-decoration: none;
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
        .nav-item i {
            width: 18px;
            height: 18px;
        }
        .sidebar-footer {
            padding: 1.5rem;
            border-top: 1px solid var(--border-light);
            font-size: 0.85rem;
            color: var(--text-muted);
        }

        /* --- MAIN LAYOUT CONTEXT --- */
        main {
            margin-left: 260px;
            flex: 1;
            padding: 2.5rem;
            max-width: 1400px;
        }
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2.5rem;
        }
        h2.page-title {
            font-family: var(--font-heading);
            font-size: 2.25rem;
            color: var(--text-main);
        }

        /* --- UTILITIES & UI COMPONENTS --- */
        .btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 0.75rem 1.25rem;
            font-family: var(--font-ui);
            font-weight: 600;
            border-radius: var(--radius);
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: var(--transition);
        }
        .btn:hover {
            background-color: var(--primary-hover);
        }
        .btn-secondary {
            background-color: transparent;
            border: 1px solid var(--border-light);
            color: var(--text-main);
        }
        .btn-secondary:hover {
            background-color: var(--bg-warm);
        }

        /* Input Controls */
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
            border: 1px solid var(--border-light);
            border-radius: var(--radius);
            outline: none;
            background-color: var(--bg-warm);
            transition: var(--transition);
        }
        .form-control:focus {
            border-color: var(--accent);
            background-color: var(--surface);
        }

        /* Stat Grid Cards */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2.5rem;
        }
        .stat-card {
            background: var(--surface);
            border: 1px solid var(--border-light);
            border-radius: var(--radius);
            padding: 1.5rem;
            position: relative;
        }
        .stat-label {
            font-size: 0.85rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.05em;
            margin-bottom: 0.5rem;
        }
        .stat-value {
            font-family: var(--font-heading);
            font-size: 1.85rem;
            font-weight: 600;
            color: var(--text-main);
        }
        .stat-footer {
            margin-top: 0.75rem;
            font-size: 0.8rem;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        /* Data Tables */
        .table-container {
            background: var(--surface);
            border: 1px solid var(--border-light);
            border-radius: var(--radius);
            overflow: hidden;
            margin-bottom: 2.5rem;
        }
        .table-header {
            padding: 1.5rem;
            border-bottom: 1px solid var(--border-light);
            display: flex;
            justify-content: space-between;
            align-items: center;
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
            font-weight: 600;
            color: var(--text-muted);
            border-bottom: 1px solid var(--border-light);
        }
        td {
            padding: 1.25rem 1.5rem;
            border-bottom: 1px solid var(--border-light);
            color: var(--text-main);
        }
        tr:last-child td {
            border-bottom: none;
        }

        /* Status Pills */
        .pill {
            display: inline-flex;
            align-items: center;
            padding: 0.25rem 0.75rem;
            border-radius: 50px;
            font-size: 0.75rem;
            font-weight: 600;
        }
        .pill-serving { background-color: var(--warning-light); color: var(--warning); }
        .pill-served { background-color: var(--accent-light); color: var(--accent); }
        .pill-paid { background-color: var(--success-light); color: var(--success); }

        /* App Sections Views Visibility toggle */
        .app-view {
            display: none;
        }
        .app-view.active-view {
            display: block;
        }

        /* Two Column Layout Split */
        .dashboard-split {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 1.5rem;
        }

        /* Chart Visual Placeholder Components */
        .chart-placeholder {
            background: linear-gradient(180deg, var(--bg-warm) 0%, #FFFFFF 100%);
            border: 1px dashed var(--border-light);
            border-radius: var(--radius);
            height: 220px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            font-size: 0.85rem;
        }
    </style>
</head>
<body>

    <div id="login-overlay">
        <div class="login-hero">
            <h1>ROTISSERIE</h1>
            <p>College Tiniali, Golaghat, Assam 785621</p>
        </div>
        <div class="login-form-container">
            <div class="login-brand">ROTISSERIE Engine</div>
            <div class="login-subtitle">Secure Custom JWT Operational Access</div>
            <form onsubmit="handleLogin(event)">
                <div class="form-group">
                    <label>Operational Role / User ID</label>
                    <input type="text" class="form-control" placeholder="e.g., admin_golaghat" required value="admin_golaghat">
                </div>
                <div class="form-group">
                    <label>Secret Passkey</label>
                    <input type="password" class="form-control" placeholder="••••••••" required value="password123">
                </div>
                <button type="submit" class="btn" style="width: 100%; justify-content: center; margin-top: 1rem;">
                    Sign In & Verify JWT <i data-lucide="shield-check"></i>
                </button>
            </form>
        </div>
    </div>

    <aside>
        <div class="sidebar-header">
            <div class="sidebar-brand">ROTISSERIE</div>
            <div class="sidebar-location">Golaghat, Assam (ID: 785621)</div>
        </div>
        <ul class="nav-list">
            <li class="nav-item active" onclick="switchView('dashboard', this)"><i data-lucide="layout-dashboard"></i>Dashboard</li>
            <li class="nav-item" onclick="switchView('orders', this)"><i data-lucide="utensils-crossedd"></i>Active Orders</li>
            <li class="nav-item" onclick="switchView('inventory', this)"><i data-lucide="boxes"></i>Inventory Assets</li>
            <li class="nav-item" onclick="switchView('staff', this)"><i data-lucide="users"></i>Staff Registry</li>
            <li class="nav-item" onclick="switchView('customers', this)"><i data-lucide="heart-handshake"></i>Guests & Ratings</li>
        </ul>
        <div class="sidebar-footer">
            <p style="font-weight:600; margin-bottom:4px;">Secure Token Context</p>
            <p id="jwt-badge" style="font-family: monospace; font-size:11px; word-break: break-all; opacity: 0.7;">No Session</p>
        </div>
    </aside>

    <main>
        
        <div id="view-dashboard" class="app-view active-view">
            <header>
                <div>
                    <h2 class="page-title">Operational Overview</h2>
                    <p style="color: var(--text-muted); font-size: 0.9rem;">Real-time metrics for Golaghat hub</p>
                </div>
                <button class="btn" onclick="switchView('orders')"><i data-lucide="plus"></i> New Order Entry</button>
            </header>

            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-label">Net Daily Profit</div>
                    <div class="stat-value">₹14,250</div>
                    <div class="stat-footer" style="color: var(--success);"><i data-lucide="trending-up"></i> +12% from yesterday</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Total Liquid Cash</div>
                    <div class="stat-value">₹32,840</div>
                    <div class="stat-footer"><i data-lucide="wallet"></i> Drawer balance verified</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Avg Service Time</div>
                    <div class="stat-value">14.2 min</div>
                    <div class="stat-footer" style="color: var(--success);"><i data-lucide="zap"></i> -2 min optimizations</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Aggregate Rating</div>
                    <div class="stat-value">4.6 / 5</div>
                    <div class="stat-footer" style="color: var(--accent);"><i data-lucide="star"></i> 48 guest responses</div>
                </div>
            </div>

            <div class="dashboard-split">
                <div class="table-container" style="margin-bottom:0;">
                    <div class="table-header"><h3>Active Kitchen Track</h3></div>
                    <table>
                        <thead>
                            <tr>
                                <th>Table / Token</th>
                                <th>Item Ordered</th>
                                <th>Service Clock</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Table 4A</td>
                                <td>Quarter Classic Roasted Chicken</td>
                                <td>8 mins elapsed</td>
                                <td><span class="pill pill-serving">Serving</span></td>
                            </tr>
                            <tr>
                                <td>Takeaway Token #12</td>
                                <td>Full Wood-Fired Spiced Platter</td>
                                <td>16 mins elapsed</td>
                                <td><span class="pill pill-served">Served</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <div class="table-container" style="margin-bottom:0; padding:1.5rem;">
                    <h3 style="margin-bottom: 1rem;">Daily Profit Line</h3>
                    <div class="chart-placeholder">[ Interactive Profit Timeline Area ]</div>
                </div>
            </div>
        </div>

        <div id="view-orders" class="app-view">
            <header>
                <div>
                    <h2 class="page-title">Order Processing Matrix</h2>
                    <p style="color: var(--text-muted); font-size: 0.9rem;">Track kitchen cycles, ticket windows, and guest payout settlements</p>
                </div>
            </header>

            <div class="dashboard-split" style="grid-template-columns: 1fr 2fr;">
                <div class="table-container" style="padding: 1.5rem; background: #FFFFFF; height: fit-content;">
                    <h3 style="margin-bottom:1.25rem; font-family: var(--font-heading);">Generate Live Ticket</h3>
                    <form onsubmit="addMockOrder(event)">
                        <div class="form-group">
                            <label>Menu Variant Selection</label>
                            <select class="form-control" id="order-item">
                                <option value="Classic Half Roasted Chicken">Classic Half Roasted Chicken — ₹240</option>
                                <option value="Spiced Quarter Breast">Spiced Quarter Breast — ₹140</option>
                                <option value="Full Banquet Platter">Full Banquet Platter — ₹450</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Service Channel / Table Mark</label>
                            <input type="text" class="form-control" id="order-table" placeholder="e.g., Table 3, Quick Counter" required>
                        </div>
                        <div class="form-group">
                            <label>Voluntary Customer Gratuity (Tips - ₹)</label>
                            <input type="number" class="form-control" id="order-tips" placeholder="0" value="20">
                        </div>
                        <button type="submit" class="btn" style="width:100%; justify-content:center;">Commit Ticket to Matrix</button>
                    </form>
                </div>

                <div class="table-container">
                    <div class="table-header"><h3>Active Floor Register</h3></div>
                    <table id="orders-table">
                        <thead>
                            <tr>
                                <th>Order Ref</th>
                                <th>Target Location</th>
                                <th>Menu Item</th>
                                <th>Total Bill</th>
                                <th>Tips Handover</th>
                                <th>Current Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>#ROT-9821</td>
                                <td>Table 2</td>
                                <td>Classic Half Roasted Chicken</td>
                                <td>₹240</td>
                                <td>₹30</td>
                                <td><span class="pill pill-paid">Paid</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <div id="view-inventory" class="app-view">
            <header>
                <div>
                    <h2 class="page-title">Stock &amp; Raw Assets</h2>
                    <p style="color: var(--text-muted); font-size: 0.9rem;">Warehouse quantities and critical low-stock alert infrastructure</p>
                </div>
            </header>
            <div class="table-container">
                <div class="table-header"><h3>Central Kitchen Stock Ledger</h3></div>
                <table>
                    <thead>
                        <tr>
                            <th>Ingredient Component</th>
                            <th>Storage Class</th>
                            <th>In-Store Baseline Vol</th>
                            <th>Safety Index Metric</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Fresh Broiler Chicken Hub Units</td>
                            <td>Refrigerated Storage Alpha</td>
                            <td>42 Kgs</td>
                            <td><span class="pill pill-paid">Optimal</span></td>
                        </tr>
                        <tr>
                            <td>Assam Organic Firewood Packs</td>
                            <td>Dry Storage Yard</td>
                            <td>8 Bundles</td>
                            <td><span class="pill pill-serving">Low Stock Alert</span></td>
                        </tr>
                        <tr>
                            <td>House Secret Marinade Compound</td>
                            <td>Cold Vault Beta</td>
                            <td>15 Liters</td>
                            <td><span class="pill pill-paid">Optimal</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <div id="view-staff" class="app-view">
            <header>
                <div>
                    <h2 class="page-title">Staff Workspace Configuration</h2>
                    <p style="color: var(--text-muted); font-size: 0.9rem;">Configure user account system permissions, shifts, and operations tasks</p>
                </div>
            </header>
            <div class="table-container">
                <div class="table-header"><h3>Active Workforce Registry</h3></div>
                <table>
                    <thead>
                        <tr>
                            <th>Staff Member Name</th>
                            <th>Assigned Operations Duty Role</th>
                            <th>Active Shift Allocation</th>
                            <th>System Auth Token Status</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Jitendra Gogoi</td>
                            <td>Head Kitchen Master Roaster</td>
                            <td>Day Prep Core (08:00 - 16:00)</td>
                            <td><span class="pill pill-paid">Verified JWT Admin</span></td>
                        </tr>
                        <tr>
                            <td>Prashant Saikia</td>
                            <td>Floor Lead &amp; Cashier Steward</td>
                            <td>Evening Rush Core (15:00 - 23:00)</td>
                            <td><span class="pill pill-served">Staff Level Access</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <div id="view-customers" class="app-view">
            <header>
                <div>
                    <h2 class="page-title">Customer Feedback Ledger</h2>
                    <p style="color: var(--text-muted); font-size: 0.9rem;">Aggregate reviews, average platform ratings, and historical loyalty tracks</p>
                </div>
            </header>
            <div class="table-container">
                <div class="table-header"><h3>Recent Customer Accounts</h3></div>
                <table>
                    <thead>
                        <tr>
                            <th>Guest Identifier</th>
                            <th>Frequency Track</th>
                            <th>Assigned Rating Record</th>
                            <th>Steward Commentary Context</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Ananya B. (Counter Guest)</td>
                            <td>Frequent Core Regular</td>
                            <td>⭐⭐⭐⭐⭐ 5.0</td>
                            <td>Expressed high preference for the wood-fired spice glaze mix.</td>
                        </tr>
                        <tr>
                            <td>Rituraj D. (Table 5)</td>
                            <td>First-time Diner Visit</td>
                            <td>⭐⭐⭐⭐ 4.0</td>
                            <td>Noted table service time during peak rush hour was satisfactory.</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

    </main>

    <script>
        // Simulate execution of standard payload encryption signature validation pattern
        window.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
        });

        function handleLogin(event) {
            event.preventDefault();
            // Generate standard cryptographic UI visual placeholder to match JWT request simulation parameters
            const sampleJWT = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiUm90aXNzZXJpZSBG&b29kIiwicm9sZSI6ImFkbWluIiwiZXhwIjoyNTM0MDIzMDAwMDB9.s7X_bW9";
            document.getElementById('jwt-badge').innerText = sampleJWT;
            
            // Smoothly remove overlay panel interface mask context component from dynamic viewport view DOM hierarchy
            const overlay = document.getElementById('login-overlay');
            overlay.style.opacity = '0';
            setTimeout(() => { overlay.style.display = 'none'; }, 200);
        }

        function switchView(viewId, element) {
            // Hide all active visibility canvas zones completely using target selector loops
            const views = document.querySelectorAll('.app-view');
            views.forEach(view => view.classList.remove('active-view'));
            
            // Re-activate specific targeted operational view sector safely inside layout document DOM tree context
            const targetedView = document.getElementById('view-' + viewId);
            if(targetedView) {
                targetedView.classList.add('active-view');
            }

            // Clean existing primary navigational component highlight states from DOM element styles
            if(element) {
                const items = document.querySelectorAll('.nav-item');
                items.forEach(item => item.classList.remove('active'));
                element.classList.add('active');
            }
        }

        function addMockOrder(event) {
            event.preventDefault();
            const itemElement = document.getElementById('order-item');
            const itemText = itemElement.options[itemElement.selectedIndex].text.split(' — ')[0];
            const priceText = itemElement.options[itemElement.selectedIndex].text.split(' — ')[1];
            const tableMark = document.getElementById('order-table').value;
            const tipsAmount = document.getElementById('order-tips').value;

            const tableRef = document.getElementById('orders-table').getElementsByTagName('tbody')[0];
            const newRow = tableRef.insertRow(0);

            newRow.innerHTML = `
                <td>#ROT-${Math.floor(1000 + Math.random() * 9000)}</td>
                <td>${tableMark}</td>
                <td>${itemText}</td>
                <td>${priceText}</td>
                <td>₹${tipsAmount || 0}</td>
                <td><span class="pill pill-serving">Serving</span></td>
            `;
            
            // Clear inputs for next operation cycle execution step pattern
            document.getElementById('order-table').value = '';
        }
    </script>
</body>
</html>
