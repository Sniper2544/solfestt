<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Solfest · Ticket Collection (Pochi la Biashara)</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', 'Segoe UI', Roboto, system-ui, sans-serif;
            background: linear-gradient(145deg, #1a1e2b 0%, #2a1f2d 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 1.5rem;
        }

        .ticket-card {
            max-width: 1000px;
            width: 100%;
            background: rgba(22, 26, 35, 0.85);
            backdrop-filter: blur(12px);
            border-radius: 3rem;
            box-shadow: 0 30px 50px rgba(0, 0, 0, 0.7), 0 0 0 1px rgba(255, 215, 0, 0.15);
            border: 1px solid rgba(255, 215, 0, 0.2);
            overflow: hidden;
            transition: all 0.2s;
        }

        .event-panel {
            display: grid;
            grid-template-columns: 1.2fr 1fr;
            gap: 0;
        }

        .brand-side {
            padding: 3rem 2.5rem;
            background: radial-gradient(circle at 20% 30%, #3e2b1f, #1a1210);
            display: flex;
            flex-direction: column;
            justify-content: center;
            border-right: 1px dashed rgba(255, 215, 0, 0.3);
            position: relative;
        }

        .brand-side::after {
            content: "🎫";
            position: absolute;
            bottom: 1.5rem;
            right: 2rem;
            font-size: 4rem;
            opacity: 0.1;
            transform: rotate(15deg);
            pointer-events: none;
        }

        .fest-title {
            font-size: 5.5rem;
            font-weight: 900;
            line-height: 1;
            letter-spacing: -0.02em;
            text-transform: uppercase;
            color: #f5e7c8;
            text-shadow: 0 4px 20px rgba(255, 180, 40, 0.5), 0 0 0 2px #b8860b;
            margin-bottom: 0.5rem;
        }

        .fest-sub {
            font-size: 1.1rem;
            font-weight: 500;
            letter-spacing: 0.3em;
            color: #e0b354;
            text-transform: uppercase;
            margin-top: 0.25rem;
            border-left: 3px solid #e0b354;
            padding-left: 1rem;
        }

        .date-venue {
            margin-top: 2.5rem;
            color: #cbbfaf;
            display: flex;
            flex-direction: column;
            gap: 0.6rem;
            font-size: 1.1rem;
            border-top: 1px solid rgba(224, 179, 84, 0.3);
            padding-top: 1.8rem;
        }

        .date-venue i {
            color: #e0b354;
            width: 1.8rem;
            font-size: 1.2rem;
        }

        .date-venue span {
            font-weight: 400;
            display: flex;
            align-items: center;
            gap: 0.8rem;
        }

        /* RIGHT SIDE — purchase + payment */
        .purchase-side {
            background: #0f1117;
            padding: 2rem 1.8rem;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .price-tag {
            display: flex;
            align-items: baseline;
            gap: 0.5rem;
            margin-bottom: 1.5rem;
            background: rgba(224, 179, 84, 0.05);
            padding: 0.8rem 1.2rem;
            border-radius: 100px;
            border: 1px solid rgba(224, 179, 84, 0.2);
            width: fit-content;
        }

        .price-tag .currency {
            font-size: 1.1rem;
            font-weight: 500;
            color: #e0b354;
        }

        .price-tag .amount {
            font-size: 2.6rem;
            font-weight: 800;
            color: #fff4e0;
            letter-spacing: -0.02em;
            line-height: 1;
        }

        .price-tag .per-ticket {
            color: #8a7e6e;
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .pochi-badge {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            background: #1e2a1b;
            border: 1px solid #3e6b3a;
            padding: 0.5rem 1rem;
            border-radius: 40px;
            margin-bottom: 1.2rem;
            font-size: 0.85rem;
            color: #b6e2b0;
            width: fit-content;
        }

        .pochi-badge i {
            color: #4caf50;
        }

        .pochi-badge strong {
            color: #e0b354;
            font-weight: 700;
            letter-spacing: 0.5px;
        }

        .buyer-form {
            display: flex;
            flex-direction: column;
            gap: 0.9rem;
            margin-bottom: 1.2rem;
        }

        .input-group {
            display: flex;
            flex-direction: column;
            gap: 0.25rem;
        }

        .input-group label {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            font-weight: 600;
            color: #b8a58b;
            margin-left: 0.25rem;
        }

        .input-group input {
            background: #1e212b;
            border: 1px solid #373d4a;
            border-radius: 60px;
            padding: 0.8rem 1.3rem;
            font-size: 0.95rem;
            color: #f0ece4;
            outline: none;
            transition: 0.2s;
            font-family: inherit;
        }

        .input-group input:focus {
            border-color: #e0b354;
            box-shadow: 0 0 0 3px rgba(224, 179, 84, 0.2);
            background: #1a1e26;
        }

        .input-group input::placeholder {
            color: #5d5f6b;
            font-weight: 300;
        }

        .input-group input:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }

        .action-row {
            display: flex;
            align-items: center;
            gap: 0.8rem;
            margin: 0.3rem 0 1rem;
        }

        .qty-selector {
            display: flex;
            align-items: center;
            background: #1e212b;
            border-radius: 60px;
            border: 1px solid #373d4a;
            padding: 0.15rem;
        }

        .qty-btn {
            background: transparent;
            border: none;
            color: #e0b354;
            font-size: 1.3rem;
            font-weight: 600;
            width: 2.2rem;
            height: 2.2rem;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: 0.1s;
            font-family: inherit;
        }

        .qty-btn:hover:not(:disabled) {
            background: rgba(224, 179, 84, 0.15);
        }

        .qty-btn:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }

        .qty-display {
            width: 2.2rem;
            text-align: center;
            font-weight: 600;
            font-size: 1.1rem;
            color: #f0ece4;
        }

        .pay-btn {
            flex: 1;
            background: linear-gradient(135deg, #e0b354, #c99a2e);
            border: none;
            border-radius: 60px;
            padding: 0.8rem 1rem;
            font-size: 0.9rem;
            font-weight: 700;
            color: #1a1210;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            transition: all 0.2s;
            box-shadow: 0 6px 15px rgba(224, 179, 84, 0.25);
            font-family: inherit;
            white-space: nowrap;
        }

        .pay-btn i {
            font-size: 1rem;
        }

        .pay-btn:hover:not(:disabled) {
            background: linear-gradient(135deg, #efc56b, #d4a53a);
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(224, 179, 84, 0.35);
        }

        .pay-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .pay-btn:active:not(:disabled) {
            transform: translateY(2px);
            box-shadow: 0 4px 10px rgba(224, 179, 84, 0.25);
        }

        .collection-area {
            background: #0b0d12;
            border-radius: 2rem;
            padding: 1rem 1rem 0.8rem;
            margin-top: 0.3rem;
            border: 1px solid #262b36;
            transition: all 0.2s;
        }

        .collection-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.7rem;
            padding: 0 0.2rem;
        }

        .collection-header h3 {
            font-size: 0.8rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            color: #8f8779;
            font-weight: 600;
        }

        .clear-btn {
            background: none;
            border: none;
            color: #b84a4a;
            font-size: 0.65rem;
            text-transform: uppercase;
            font-weight: 600;
            letter-spacing: 0.5px;
            cursor: pointer;
            padding: 0.2rem 0.5rem;
            border-radius: 30px;
            transition: 0.2s;
            display: flex;
            align-items: center;
            gap: 0.3rem;
        }

        .clear-btn i {
            font-size: 0.65rem;
        }

        .clear-btn:hover {
            background: rgba(184, 74, 74, 0.15);
        }

        .ticket-list {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
            max-height: 140px;
            overflow-y: auto;
            padding-right: 0.3rem;
            scrollbar-width: thin;
            scrollbar-color: #e0b354 #1e212b;
        }

        .ticket-list::-webkit-scrollbar {
            width: 5px;
        }

        .ticket-list::-webkit-scrollbar-track {
            background: #1e212b;
            border-radius: 10px;
        }

        .ticket-list::-webkit-scrollbar-thumb {
            background: #e0b354;
            border-radius: 10px;
        }

        .ticket-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #171b24;
            padding: 0.55rem 0.9rem;
            border-radius: 60px;
            border-left: 4px solid #e0b354;
            font-size: 0.85rem;
            animation: fadeIn 0.25s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-6px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .ticket-info {
            display: flex;
            flex-direction: column;
        }

        .ticket-owner {
            font-weight: 600;
            color: #f0e2cc;
            font-size: 0.85rem;
        }

        .ticket-code {
            font-size: 0.65rem;
            color: #9b8f7e;
            letter-spacing: 0.5px;
            font-family: monospace;
        }

        .ticket-price-badge {
            background: rgba(224, 179, 84, 0.15);
            padding: 0.2rem 0.7rem;
            border-radius: 30px;
            font-size: 0.75rem;
            font-weight: 600;
            color: #e0b354;
            white-space: nowrap;
        }

        .empty-collection {
            color: #4f5563;
            font-size: 0.85rem;
            text-align: center;
            padding: 1rem 0.5rem;
            font-style: italic;
        }

        .toast-message {
            font-size: 0.75rem;
            color: #e0b354;
            text-align: center;
            margin-top: 0.5rem;
            min-height: 1.1rem;
            transition: 0.2s;
            font-weight: 400;
        }

        /* ----- MPESA PIN MODAL ----- */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(6px);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 1.5rem;
        }

        .modal-overlay.active {
            display: flex;
        }

        .mpesa-modal {
            background: #1a1e26;
            border-radius: 2.5rem;
            padding: 2rem 1.8rem;
            max-width: 420px;
            width: 100%;
            border: 1px solid #3e4a3c;
            box-shadow: 0 40px 70px rgba(0, 0, 0, 0.8), 0 0 0 1px #4caf5040;
            animation: modalSlide 0.25s ease;
        }

        @keyframes modalSlide {
            from { opacity: 0; transform: translateY(30px) scale(0.95); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }

        .mpesa-header {
            display: flex;
            align-items: center;
            gap: 0.8rem;
            margin-bottom: 1.5rem;
        }

        .mpesa-header i {
            font-size: 2.2rem;
            color: #4caf50;
        }

        .mpesa-header h3 {
            color: #e8f0e6;
            font-size: 1.3rem;
            font-weight: 700;
        }

        .mpesa-header span {
            display: block;
            font-size: 0.75rem;
            color: #8a9a86;
            font-weight: 400;
            letter-spacing: 0.5px;
            margin-top: 0.15rem;
        }

        .payment-summary {
            background: #0f1318;
            border-radius: 1.5rem;
            padding: 1rem 1.2rem;
            margin-bottom: 1.5rem;
            border: 1px solid #2b332a;
        }

        .summary-row {
            display: flex;
            justify-content: space-between;
            font-size: 0.85rem;
            color: #a8b3a5;
            padding: 0.3rem 0;
        }

        .summary-row.total {
            font-weight: 700;
            color: #e0b354;
            font-size: 1rem;
            border-top: 1px dashed #3e4a3c;
            margin-top: 0.3rem;
            padding-top: 0.6rem;
        }

        .summary-row strong {
            color: #f0ece4;
        }

        .pin-input-group {
            display: flex;
            flex-direction: column;
            gap: 0.4rem;
            margin-bottom: 1.5rem;
        }

        .pin-input-group label {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: #b8a58b;
            font-weight: 600;
        }

        .pin-input-group input {
            background: #0d1015;
            border: 1.5px solid #3e4a3c;
            border-radius: 60px;
            padding: 0.9rem 1.4rem;
            font-size: 1.4rem;
            letter-spacing: 0.6rem;
            color: #f0ece4;
            font-family: monospace;
            text-align: center;
            outline: none;
            transition: 0.2s;
        }

        .pin-input-group input:focus {
            border-color: #4caf50;
            box-shadow: 0 0 0 3px rgba(76, 175, 80, 0.2);
        }

        .pin-input-group input::placeholder {
            letter-spacing: 0.2rem;
            font-size: 0.9rem;
            color: #4a5550;
        }

        .modal-actions {
            display: flex;
            gap: 0.8rem;
        }

        .modal-btn {
            flex: 1;
            border: none;
            border-radius: 60px;
            padding: 0.9rem;
            font-size: 0.85rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            cursor: pointer;
            transition: 0.2s;
            font-family: inherit;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.4rem;
        }

        .modal-btn.cancel {
            background: #2a2f3a;
            color: #b0b8c5;
        }

        .modal-btn.cancel:hover {
            background: #353b48;
        }

        .modal-btn.confirm {
            background: linear-gradient(135deg, #4caf50, #3d8b40);
            color: #fff;
            box-shadow: 0 6px 15px rgba(76, 175, 80, 0.3);
        }

        .modal-btn.confirm:hover {
            background: linear-gradient(135deg, #5fcf63, #4a9e4e);
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(76, 175, 80, 0.4);
        }

        .modal-btn.confirm:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .pin-hint {
            font-size: 0.65rem;
            color: #6a7a66;
            text-align: center;
            margin-top: 0.8rem;
            letter-spacing: 0.3px;
        }

        .processing-spinner {
            display: inline-block;
            width: 1rem;
            height: 1rem;
            border: 2px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            border-top-color: #fff;
            animation: spin 0.6s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* responsive */
        @media (max-width: 750px) {
            .event-panel {
                grid-template-columns: 1fr;
            }
            .brand-side {
                border-right: none;
                border-bottom: 1px dashed rgba(255, 215, 0, 0.3);
                padding: 2rem 1.8rem;
            }
            .fest-title {
                font-size: 4rem;
            }
            .purchase-side {
                padding: 1.8rem 1.3rem;
            }
            .ticket-card {
                border-radius: 2rem;
            }
        }

        @media (max-width: 450px) {
            .fest-title {
                font-size: 3rem;
            }
            .price-tag .amount {
                font-size: 2.2rem;
            }
            .action-row {
                flex-wrap: wrap;
            }
            .mpesa-modal {
                padding: 1.5rem 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="ticket-card">
        <div class="event-panel">
            <!-- left: brand / event info -->
            <div class="brand-side">
                <div class="fest-title">SOLFEST</div>
                <div class="fest-sub">2025 · live music</div>
                <div class="date-venue">
                    <span><i class="fas fa-calendar-alt"></i> Saturday, Dec 13, 2025</span>
                    <span><i class="fas fa-map-pin"></i> Waterfront Arena, Nairobi</span>
                    <span><i class="fas fa-clock"></i> Gates open 4:00 PM</span>
                </div>
            </div>

            <!-- right: purchase + payment -->
            <div class="purchase-side">
                <div class="price-tag">
                    <span class="currency">Kshs</span>
                    <span class="amount">1500</span>
                    <span class="per-ticket">/ ticket</span>
                </div>

                <!-- Pochi la Biashara number -->
                <div class="pochi-badge">
                    <i class="fas fa-mobile-alt"></i>
                    <span>Pay via <strong>Pochi la Biashara</strong> · <strong>0743393815</strong></span>
                </div>

                <!-- buyer name form -->
                <div class="buyer-form">
                    <div class="input-group">
                        <label for="buyerName">Full name</label>
                        <input type="text" id="buyerName" placeholder="e.g. John Mwangi" autocomplete="off">
                    </div>
                </div>

                <!-- quantity + collect button -->
                <div class="action-row">
                    <div class="qty-selector">
                        <button class="qty-btn" id="decrementQty" aria-label="Decrease quantity" disabled>−</button>
                        <span class="qty-display" id="qtyDisplay">1</span>
                        <button class="qty-btn" id="incrementQty" aria-label="Increase quantity">+</button>
                    </div>
                    <button class="pay-btn" id="collectBtn">
                        <i class="fas fa-ticket-alt"></i> Collect
                    </button>
                </div>

                <!-- collected tickets list -->
                <div class="collection-area">
                    <div class="collection-header">
                        <h3><i class="fas fa-receipt" style="margin-right: 6px;"></i> Your tickets</h3>
                        <button class="clear-btn" id="clearAllBtn"><i class="fas fa-trash-alt"></i> clear</button>
                    </div>
                    <div class="ticket-list" id="ticketList">
                        <div class="empty-collection">No tickets collected yet</div>
                    </div>
                    <div class="toast-message" id="toastMsg"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- ---------- MPESA PIN MODAL ---------- -->
    <div class="modal-overlay" id="pinModal">
        <div class="mpesa-modal">
            <div class="mpesa-header">
                <i class="fas fa-shield-alt"></i>
                <div>
                    <h3>M-Pesa PIN</h3>
                    <span>Enter your PIN to complete payment</span>
                </div>
            </div>

            <div class="payment-summary">
                <div class="summary-row">
                    <span>Pay to</span>
                    <strong>Pochi la Biashara</strong>
                </div>
                <div class="summary-row">
                    <span>Number</span>
                    <strong>0743393815</strong>
                </div>
                <div class="summary-row">
                    <span>Quantity</span>
                    <strong id="modalQty">1</strong>
                </div>
                <div class="summary-row">
                    <span>Price per ticket</span>
                    <strong>Kshs 1,500</strong>
                </div>
                <div class="summary-row total">
                    <span>Total</span>
                    <strong id="modalTotal">Kshs 1,500</strong>
                </div>
            </div>

            <div class="pin-input-group">
                <label for="mpesaPin">M-Pesa PIN</label>
                <input type="password" id="mpesaPin" maxlength="4" placeholder="••••" inputmode="numeric" autocomplete="off">
            </div>

            <div class="modal-actions">
                <button class="modal-btn cancel" id="cancelPaymentBtn">Cancel</button>
                <button class="modal-btn confirm" id="confirmPaymentBtn">
                    <i class="fas fa-check-circle"></i> Confirm
                </button>
            </div>
            <div class="pin-hint">🔒 Your PIN is only used for this demo payment simulation.</div>
        </div>
    </div>

    <script>
        (function() {
            // ---------- constants ----------
            const TICKET_PRICE = 1500;          // Kshs
            const CURRENCY = 'Kshs';
            const POCHI_NUMBER = '0743393815';

            // ---------- state ----------
            let tickets = [];                    // collected ticket objects
            let currentQty = 1;                  // selected quantity
            let pendingPurchase = null;          // { name, qty } while waiting for PIN

            // ---------- DOM elements ----------
            const buyerNameInput = document.getElementById('buyerName');
            const qtyDisplay = document.getElementById('qtyDisplay');
            const decrementBtn = document.getElementById('decrementQty');
            const incrementBtn = document.getElementById('incrementQty');
            const collectBtn = document.getElementById('collectBtn');
            const ticketListEl = document.getElementById('ticketList');
            const clearAllBtn = document.getElementById('clearAllBtn');
            const toastMsg = document.getElementById('toastMsg');

            // modal
            const pinModal = document.getElementById('pinModal');
            const mpesaPinInput = document.getElementById('mpesaPin');
            const modalQty = document.getElementById('modalQty');
            const modalTotal = document.getElementById('modalTotal');
            const cancelPaymentBtn = document.getElementById('cancelPaymentBtn');
            const confirmPaymentBtn = document.getElementById('confirmPaymentBtn');

            // ---------- helpers ----------
            function generateTicketCode() {
                return 'SLF-' + Math.random().toString(36).substring(2, 8).toUpperCase() +
                       '-' + (Math.floor(Math.random() * 9000) + 1000);
            }

            function showToast(text, isError = false) {
                toastMsg.textContent = text;
                toastMsg.style.color = isError ? '#f87171' : '#e0b354';
                if (window.toastTimer) clearTimeout(window.toastTimer);
                window.toastTimer = setTimeout(() => {
                    toastMsg.textContent = '';
                }, 3000);
            }

            function escapeHtml(text) {
                const div = document.createElement('div');
                div.textContent = text;
                return div.innerHTML;
            }

            function renderTickets() {
                if (!ticketListEl) return;
                if (tickets.length === 0) {
                    ticketListEl.innerHTML = `<div class="empty-collection">No tickets collected yet</div>`;
                    return;
                }
                let html = '';
                tickets.forEach((ticket) => {
                    html += `
                        <div class="ticket-item">
                            <div class="ticket-info">
                                <span class="ticket-owner">${escapeHtml(ticket.owner)}</span>
                                <span class="ticket-code">${ticket.code}</span>
                            </div>
                            <span class="ticket-price-badge">${CURRENCY} ${ticket.price}</span>
                        </div>
                    `;
                });
                ticketListEl.innerHTML = html;
            }

            function updateQuantityUI() {
                qtyDisplay.textContent = currentQty;
                decrementBtn.disabled = (currentQty <= 1);
                incrementBtn.disabled = (currentQty >= 10);
            }

            // ---------- modal open/close ----------
            function openPinModal(purchase) {
                pendingPurchase = purchase;
                modalQty.textContent = purchase.qty;
                modalTotal.textContent = `${CURRENCY} ${(purchase.qty * TICKET_PRICE).toLocaleString()}`;
                mpesaPinInput.value = '';
                confirmPaymentBtn.disabled = false;
                confirmPaymentBtn.innerHTML = '<i class="fas fa-check-circle"></i> Confirm';
                pinModal.classList.add('active');
                // small delay so the modal is visible before focusing
                setTimeout(() => mpesaPinInput.focus(), 150);
            }

            function closePinModal() {
                pinModal.classList.remove('active');
                pendingPurchase = null;
                mpesaPinInput.value = '';
                // re-enable collect button in case it was disabled
                collectBtn.disabled = false;
                collectBtn.innerHTML = '<i class="fas fa-ticket-alt"></i> Collect';
            }

            // ---------- core actions ----------
            function initiatePayment() {
                const rawName = buyerNameInput.value.trim();

                if (rawName === '') {
                    showToast('Please enter your full name', true);
                    buyerNameInput.focus();
                    return;
                }

                if (currentQty < 1) {
                    showToast('Select at least 1 ticket', true);
                    return;
                }

                // disable collect button while modal is open
                collectBtn.disabled = true;
                collectBtn.innerHTML = '<i class="fas fa-spinner"></i> Processing…';

                // open the PIN modal
                openPinModal({ name: rawName, qty: currentQty });
            }

            function completePurchase(pin) {
                // simple PIN validation: 4 digits
                if (!/^\d{4}$/.test(pin)) {
                    showToast('Please enter a valid 4-digit M-Pesa PIN', true);
                    mpesaPinInput.focus();
                    return;
                }

                if (!pendingPurchase) {
                    closePinModal();
                    return;
                }

                const { name, qty } = pendingPurchase;

                // simulate processing state on the confirm button
                confirmPaymentBtn.disabled = true;
                confirmPaymentBtn.innerHTML = '<span class="processing-spinner"></span> Processing…';

                // simulate a short network delay for the M-Pesa prompt
                setTimeout(() => {
                    // create the tickets
                    for (let i = 0; i < qty; i++) {
                        tickets.push({
                            owner: name,
                            price: TICKET_PRICE,
                            code: generateTicketCode()
                        });
                    }

                    renderTickets();

                    const totalCost = qty * TICKET_PRICE;
                    showToast(`✅ Payment of ${CURRENCY} ${totalCost.toLocaleString()} received via Pochi la Biashara (${POCHI_NUMBER}). ${qty} ticket${qty > 1 ? 's' : ''} collected!`);

                    // reset quantity
                    currentQty = 1;
                    updateQuantityUI();

                    // close modal
                    closePinModal();

                    // restore collect button
                    collectBtn.disabled = false;
                    collectBtn.innerHTML = '<i class="fas fa-ticket-alt"></i> Collect';

                    // optionally clear name input
                    // buyerNameInput.value = '';
                }, 1200);
            }

            function clearAllTickets() {
                if (tickets.length === 0) {
                    showToast('No tickets to clear', true);
                    return;
                }
                tickets = [];
                renderTickets();
                showToast('All tickets cleared');
            }

            // ---------- event listeners ----------
            incrementBtn.addEventListener('click', () => {
                if (currentQty >= 10) {
                    showToast('Max 10 tickets per transaction', true);
                    return;
                }
                currentQty++;
                updateQuantityUI();
            });

            decrementBtn.addEventListener('click', () => {
                if (currentQty <= 1) {
                    showToast('Minimum 1 ticket', true);
                    return;
                }
                currentQty--;
                updateQuantityUI();
            });

            collectBtn.addEventListener('click', initiatePayment);

            clearAllBtn.addEventListener('click', clearAllTickets);

            buyerNameInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    initiatePayment();
                }
            });

            // modal: cancel
            cancelPaymentBtn.addEventListener('click', () => {
                closePinModal();
                showToast('Payment cancelled', true);
                collectBtn.disabled = false;
                collectBtn.innerHTML = '<i class="fas fa-ticket-alt"></i> Collect';
            });

            // modal: confirm
            confirmPaymentBtn.addEventListener('click', () => {
                const pin = mpesaPinInput.value.trim();
                completePurchase(pin);
            });

            // allow Enter key in the PIN field to confirm
            mpesaPinInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    const pin = mpesaPinInput.value.trim();
                    completePurchase(pin);
                }
            });

            // close modal by clicking on overlay background
            pinModal.addEventListener('click', (e) => {
                if (e.target === pinModal) {
                    closePinModal();
                    showToast('Payment cancelled', true);
                    collectBtn.disabled = false;
                    collectBtn.innerHTML = '<i class="fas fa-ticket-alt"></i> Collect';
                }
            });

            // initialize
            updateQuantityUI();
            renderTickets();

            // Optional: prefill demo name for quick testing
            // buyerNameInput.value = 'Demo User';
        })();
    </script>
</body>
</html># solfestt
