# flynnwifi.github.io

**SSID**: Telstra_FE9032_2G_Guest

**Password**: Y975Yc9gz4TKjuRC

<div class="row">
  <span class="label">Password</span>
  <code id="wifiPassword">Y975Yc9gz4TKjuRC</code>
  <button class="btn" type="button" data-copy-target="#wifiPassword">Copy</button>
</div>

<div id="toast" class="toast" aria-live="polite" aria-atomic="true"></div>

<style>
  .row { display:flex; align-items:center; gap:12px; flex-wrap:wrap; }
  .label { font-weight:600; min-width:90px; }
  code { padding:6px 10px; border-radius:8px; background:#f2f2f2; font-size:1rem; }
  .btn { padding:8px 12px; border-radius:10px; border:0; background:#111; color:#fff; font-weight:600; }
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
(() => {
  function toast(msg) {
    const el = document.getElementById("toast");
    if (!el) return;
    el.textContent = msg;
    el.classList.add("show");
    clearTimeout(el._t);
    el._t = setTimeout(() => el.classList.remove("show"), 1300);
  }

  function getTextFromTarget(selector) {
    const target = document.querySelector(selector);
    if (!target) return null;
    // innerText tends to match what the user sees; textContent is fine for <code>.
    const t = (target.textContent || "").trim();
    return t.length ? t : null;
  }

  async function copyToClipboard(text) {
    // Best case: modern Clipboard API (works on iOS Safari on HTTPS, triggered by tap)
    if (navigator.clipboard && window.isSecureContext) {
      await navigator.clipboard.writeText(text);
      return true;
    }

    // Fallback: execCommand (still the most compatible “old spell”)
    const ta = document.createElement("textarea");
    ta.value = text;
    ta.setAttribute("readonly", "");
    ta.style.position = "fixed";
    ta.style.top = "-1000px";
    ta.style.left = "-1000px";
    ta.style.opacity = "0";

    document.body.appendChild(ta);
    ta.focus({ preventScroll: true });
    ta.select();
    ta.setSelectionRange(0, ta.value.length); // iOS needs this

    let ok = false;
    try {
      ok = document.execCommand("copy");
    } catch (e) {
      ok = false;
    }
    document.body.removeChild(ta);
    return ok;
  }

  function attachHandlers() {
    // Event delegation: works even if you add more buttons later.
    document.addEventListener("click", async (e) => {
      const btn = e.target.closest("[data-copy-target]");
      if (!btn) return;

      e.preventDefault(); // avoid any weird default actions
      const selector = btn.getAttribute("data-copy-target");
      const text = getTextFromTarget(selector);

      if (!text) {
        toast("Nothing to copy (check the password element).");
        return;
      }

      try {
        const ok = await copyToClipboard(text);
        toast(ok ? "Copied!" : "Copy failed — tap & hold to copy");
      } catch (err) {
        toast("Copy failed — tap & hold to copy");
      }
    });
  }

  // Ensure DOM exists before binding
  if (document.readyState === "loading") {
    document.addEventListener("DOMContentLoaded", attachHandlers);
  } else {
    attachHandlers();
  }
})();
</script>

