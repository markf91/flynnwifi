# flynnwifi.github.io

**SSID**: Telstra_FE9032_2G_Guest

**Password**: Y975Yc9gz4TKjuRC

<!-- Password row -->
<div class="row">
  <span class="label">Password</span>
  <code id="wifiPassword">Y975Yc9gz4TKjuRC</code>
  <button class="btn" id="copyBtn" type="button">Copy</button>
</div>

<!-- Optional toast -->
<div id="toast" class="toast" aria-live="polite" aria-atomic="true">Copied!</div>

<style>
  .row { display:flex; align-items:center; gap:12px; flex-wrap:wrap; }
  .label { font-weight:600; min-width:90px; }
  code { padding:6px 10px; border-radius:8px; background:#f2f2f2; font-size:1rem; }
  .btn {
    padding:8px 12px; border-radius:10px; border:0;
    background:#111; color:#fff; font-weight:600;
  }
  .btn:active { transform: scale(0.98); }

  .toast{
    position: fixed; left: 50%; bottom: 24px; transform: translateX(-50%);
    background: rgba(0,0,0,0.85); color:#fff;
    padding:10px 14px; border-radius:12px;
    opacity:0; pointer-events:none; transition: opacity .2s ease;
  }
  .toast.show{ opacity:1; }
</style>

<script>
  (function () {
    const pwEl = document.getElementById('wifiPassword');
    const btn = document.getElementById('copyBtn');
    const toast = document.getElementById('toast');

    function showToast(msg) {
      if (!toast) return;
      toast.textContent = msg;
      toast.classList.add('show');
      setTimeout(() => toast.classList.remove('show'), 1200);
    }

    async function copyText(text) {
      // Best path: modern clipboard API (works on iOS Safari when page is HTTPS and user tapped button)
      if (navigator.clipboard && window.isSecureContext) {
        await navigator.clipboard.writeText(text);
        return true;
      }

      // Fallback: execCommand copy
      const ta = document.createElement('textarea');
      ta.value = text;
      ta.setAttribute('readonly', '');
      ta.style.position = 'absolute';
      ta.style.left = '-9999px';
      document.body.appendChild(ta);
      ta.select();
      ta.setSelectionRange(0, ta.value.length); // iOS support
      const ok = document.execCommand('copy');
      document.body.removeChild(ta);
      return ok;
    }

    btn.addEventListener('click', async () => {
      const text = pwEl.textContent.trim();
      try {
        const ok = await copyText(text);
        showToast(ok ? 'Copied!' : 'Copy failed — tap & hold to copy');
      } catch (e) {
        showToast('Copy failed — tap & hold to copy');
      }
    });
  })();
</script>
