
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="theme-color" content="#8A9A5B">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>Segunda Hoja</title>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --crema: #F5F0E1;
    --beige: #E8DCC4;
    --verde: #8A9A5B;
    --verde-oscuro: #6B7B3E;
    --verde-claro: #C8E6C9;
    --dorado: #D4A017;
    --naranja: #E8954A;
    --marron: #3E2723;
    --marron-claro: #5D4037;
    --blanco: #FFFFFF;
    --gris: #9E9E9E;
    --gris-claro: #F0F0F0;
    --rojo: #E53935;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
  body { font-family: 'Montserrat', sans-serif; background: #d4cdb8; }
  .sh-app {
    max-width: 420px;
    margin: 0 auto;
    min-height: 100vh;
    background: var(--crema);
    position: relative;
    overflow-x: hidden;
    padding-bottom: 80px;
  }
  .sh-screen { display: none; animation: fadeIn 0.35s ease; min-height: 100vh; }
  .sh-screen.active { display: block; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
  @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.5; } }

  /* === TOAST === */
  .sh-toast {
    position: fixed; top: 16px; left: 50%; transform: translateX(-50%) translateY(-120px);
    background: var(--marron); color: white; padding: 12px 20px; border-radius: 12px;
    font-size: 13px; font-weight: 600; z-index: 1000; transition: transform 0.35s ease;
    box-shadow: 0 8px 24px rgba(0,0,0,0.2); max-width: 90%; text-align: center;
  }
  .sh-toast.show { transform: translateX(-50%) translateY(0); }

  /* === NAV BAR === */
  .sh-nav-bar {
    position: fixed; bottom: 0; left: 50%; transform: translateX(-50%);
    width: 100%; max-width: 420px; background: var(--blanco);
    border-top: 1px solid var(--beige); display: flex; justify-content: space-around;
    padding: 8px 0 20px; z-index: 100;
  }
  .sh-nav-item {
    display: flex; flex-direction: column; align-items: center; gap: 2px;
    background: none; border: none; cursor: pointer; color: var(--gris);
    font-family: 'Montserrat', sans-serif; font-size: 10px; font-weight: 600;
    transition: color 0.2s; padding: 4px 8px;
  }
  .sh-nav-item.active { color: var(--verde); }
  .sh-nav-item .nav-icon { font-size: 22px; }

  /* === ONBOARDING === */
  .sh-onboarding { background: var(--verde); min-height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 40px 32px; text-align: center; }
  .sh-onboarding .logo-big { font-size: 80px; margin-bottom: 20px; }
  .sh-onboarding h1 { color: white; font-size: 28px; font-weight: 800; margin-bottom: 12px; }
  .sh-onboarding p { color: rgba(255,255,255,0.9); font-size: 15px; line-height: 1.6; margin-bottom: 40px; }
  .sh-dots { display: flex; gap: 8px; margin-bottom: 32px; }
  .sh-dot { width: 8px; height: 8px; background: rgba(255,255,255,0.4); border-radius: 50%; }
  .sh-dot.active { background: white; width: 24px; border-radius: 4px; }
  .sh-btn-white { width: 100%; background: white; color: var(--verde); border: none; border-radius: 14px; padding: 16px; font-family: 'Montserrat', sans-serif; font-size: 15px; font-weight: 700; cursor: pointer; box-shadow: 0 4px 16px rgba(0,0,0,0.15); }
  .sh-btn-transparent { background: none; border: 2px solid rgba(255,255,255,0.5); color: white; border-radius: 14px; padding: 14px; font-family: 'Montserrat', sans-serif; font-size: 14px; font-weight: 700; cursor: pointer; margin-top: 12px; width: 100%; }

  /* === LANDING === */
  .sh-landing-hero { background: var(--verde); padding: 32px 24px 48px; border-radius: 0 0 32px 32px; text-align: center; position: relative; overflow: hidden; }
  .sh-landing-hero::before { content: '🌿'; position: absolute; font-size: 200px; opacity: 0.06; top: -30px; right: -40px; }
  .sh-landing-logo { font-size: 48px; margin-bottom: 8px; }
  .sh-landing-hero h1 { color: white; font-size: 26px; font-weight: 800; line-height: 1.2; margin-bottom: 10px; }
  .sh-landing-hero p { color: rgba(255,255,255,0.9); font-size: 14px; font-weight: 500; line-height: 1.5; }
  .sh-landing-stats { display: flex; justify-content: center; gap: 10px; margin-top: -28px; padding: 0 16px; position: relative; z-index: 2; }
  .sh-stat-card { background: white; border-radius: 16px; padding: 14px 8px; text-align: center; box-shadow: 0 4px 16px rgba(62,39,35,0.1); flex: 1; }
  .sh-stat-card .num { font-size: 20px; font-weight: 800; color: var(--verde); display: block; }
  .sh-stat-card .lbl { font-size: 9px; color: var(--gris); font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px; }
  .sh-landing-body { padding: 24px 20px; }
  .sh-section-title { font-size: 18px; font-weight: 700; color: var(--marron); margin-bottom: 16px; }
  .sh-section-subtitle { font-size: 13px; color: var(--gris); margin-bottom: 16px; margin-top: -12px; }
  .sh-feature-list { display: flex; flex-direction: column; gap: 10px; margin-bottom: 24px; }
  .sh-feature-item { background: white; border-radius: 14px; padding: 16px; display: flex; align-items: flex-start; gap: 12px; box-shadow: 0 2px 8px rgba(0,0,0,0.04); }
  .sh-feature-icon { width: 44px; height: 44px; background: var(--beige); border-radius: 12px; display: flex; align-items: center; justify-content: center; font-size: 20px; flex-shrink: 0; }
  .sh-feature-text h4 { font-size: 13px; font-weight: 700; color: var(--marron); margin-bottom: 2px; }
  .sh-feature-text p { font-size: 12px; color: var(--gris); line-height: 1.4; }
  .sh-btn-primary { width: 100%; background: var(--verde); color: white; border: none; border-radius: 14px; padding: 16px; font-family: 'Montserrat', sans-serif; font-size: 15px; font-weight: 700; cursor: pointer; transition: all 0.2s; box-shadow: 0 4px 16px rgba(138,154,91,0.3); margin-bottom: 10px; }
  .sh-btn-primary:hover { background: var(--verde-oscuro); transform: translateY(-2px); }
  .sh-btn-secondary { width: 100%; background: transparent; color: var(--verde); border: 2px solid var(--verde); border-radius: 14px; padding: 14px; font-family: 'Montserrat', sans-serif; font-size: 14px; font-weight: 700; cursor: pointer; transition: all 0.2s; }
  .sh-btn-secondary:hover { background: var(--verde); color: white; }
  .sh-btn-small { background: var(--dorado); color: var(--marron); border: none; border-radius: 10px; padding: 10px 16px; font-family: 'Montserrat', sans-serif; font-size: 12px; font-weight: 700; cursor: pointer; }
  .sh-btn-small:hover { background: #E5B12A; }
  .sh-btn-outline-small { background: none; border: 2px solid var(--verde); color: var(--verde); border-radius: 10px; padding: 8px 14px; font-family: 'Montserrat', sans-serif; font-size: 12px; font-weight: 700; cursor: pointer; }

  /* === SIMULADOR === */
  .sh-sim-container { background: white; border-radius: 18px; padding: 20px; margin-bottom: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.04); }
  .sh-sim-label { font-size: 12px; font-weight: 700; color: var(--marron); margin-bottom: 8px; display: block; }
  .sh-slider-container { margin-bottom: 16px; }
  .sh-slider { width: 100%; -webkit-appearance: none; height: 8px; border-radius: 4px; background: var(--beige); outline: none; }
  .sh-slider::-webkit-slider-thumb { -webkit-appearance: none; width: 24px; height: 24px; border-radius: 50%; background: var(--verde); cursor: pointer; box-shadow: 0 2px 8px rgba(138,154,91,0.4); }
  .sh-slider-value { text-align: center; font-size: 28px; font-weight: 800; color: var(--verde); margin: 8px 0; }
  .sh-slider-desc { text-align: center; font-size: 12px; color: var(--gris); }
  .sh-sim-result { background: var(--verde); border-radius: 14px; padding: 20px; color: white; text-align: center; margin-top: 16px; }
  .sh-sim-result .price { font-size: 32px; font-weight: 800; }
  .sh-sim-result .period { font-size: 13px; opacity: 0.9; }
  .sh-sim-result .saving { font-size: 12px; margin-top: 8px; padding-top: 8px; border-top: 1px solid rgba(255,255,255,0.2); }

  /* === REGISTRO === */
  .sh-reg-header { background: var(--verde); padding: 20px 24px; color: white; }
  .sh-back-btn { background: none; border: none; color: white; font-size: 14px; font-weight: 700; cursor: pointer; display: flex; align-items: center; gap: 6px; margin-bottom: 12px; font-family: 'Montserrat', sans-serif; }
  .sh-reg-header h2 { font-size: 22px; font-weight: 800; }
  .sh-reg-header p { font-size: 13px; opacity: 0.9; margin-top: 4px; }
  .sh-reg-body { padding: 24px; }
  .sh-form-group { margin-bottom: 18px; }
  .sh-form-group label { display: block; font-size: 11px; font-weight: 700; color: var(--marron); margin-bottom: 6px; text-transform: uppercase; letter-spacing: 0.5px; }
  .sh-form-group input, .sh-form-group select { width: 100%; padding: 14px 16px; border: 2px solid var(--beige); border-radius: 12px; font-family: 'Montserrat', sans-serif; font-size: 14px; background: white; color: var(--marron); outline: none; transition: border-color 0.2s; }
  .sh-form-group input:focus, .sh-form-group select:focus { border-color: var(--verde); }
  .sh-plan-selector { display: flex; gap: 8px; margin-bottom: 20px; }
  .sh-plan-option { flex: 1; background: white; border: 2px solid var(--beige); border-radius: 14px; padding: 14px 6px; text-align: center; cursor: pointer; transition: all 0.2s; }
  .sh-plan-option.selected { border-color: var(--verde); background: rgba(138,154,91,0.08); }
  .sh-plan-option .plan-name { font-size: 10px; font-weight: 700; color: var(--marron); display: block; }
  .sh-plan-option .plan-price { font-size: 16px; font-weight: 800; color: var(--verde); display: block; margin: 4px 0; }
  .sh-plan-option .plan-desc { font-size: 9px; color: var(--gris); }

  /* === DASHBOARD === */
  .sh-dash-header { background: var(--verde); padding: 20px 24px 40px; color: white; position: relative; }
  .sh-dash-header::after { content: ''; position: absolute; bottom: -20px; left: 0; right: 0; height: 40px; background: var(--crema); border-radius: 24px 24px 0 0; }
  .sh-dash-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; }
  .sh-dash-top h2 { font-size: 20px; font-weight: 800; }
  .sh-dash-avatar { width: 40px; height: 40px; background: rgba(255,255,255,0.2); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 18px; }
  .sh-dash-welcome { font-size: 14px; opacity: 0.95; line-height: 1.4; }
  .sh-dash-welcome strong { font-weight: 700; }
  .sh-dash-body { padding: 0 20px 24px; position: relative; z-index: 2; }
  .sh-next-pickup { background: white; border-radius: 18px; padding: 20px; margin-bottom: 20px; box-shadow: 0 4px 20px rgba(0,0,0,0.06); border-left: 4px solid var(--dorado); }
  .sh-next-pickup .label { font-size: 11px; font-weight: 700; color: var(--dorado); text-transform: uppercase; letter-spacing: 1px; margin-bottom: 6px; }
  .sh-next-pickup .date { font-size: 20px; font-weight: 800; color: var(--marron); margin-bottom: 4px; }
  .sh-next-pickup .sub { font-size: 12px; color: var(--gris); }
  .sh-ia-badge { display: inline-flex; align-items: center; gap: 4px; background: rgba(138,154,91,0.1); color: var(--verde); padding: 4px 10px; border-radius: 10px; font-size: 10px; font-weight: 700; margin-top: 8px; }
  .sh-impact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 20px; }
  .sh-impact-card { background: white; border-radius: 16px; padding: 16px 10px; text-align: center; box-shadow: 0 2px 10px rgba(0,0,0,0.04); }
  .sh-impact-card .icon { font-size: 24px; margin-bottom: 6px; }
  .sh-impact-card .value { font-size: 22px; font-weight: 800; color: var(--marron); line-height: 1; }
  .sh-impact-card .unit { font-size: 11px; font-weight: 600; color: var(--gris); margin-bottom: 2px; }
  .sh-impact-card .desc { font-size: 10px; color: var(--gris); font-weight: 500; }
  .sh-impact-card.full-width { grid-column: 1 / -1; display: flex; align-items: center; justify-content: space-between; text-align: left; padding: 16px 20px; }
  .sh-impact-card.full-width .left { display: flex; align-items: center; gap: 12px; }
  .sh-impact-card.full-width .icon { font-size: 28px; margin: 0; }
  .sh-cert-card { background: var(--marron); border-radius: 18px; padding: 20px; color: white; margin-bottom: 20px; position: relative; overflow: hidden; }
  .sh-cert-card::before { content: '📜'; position: absolute; font-size: 80px; opacity: 0.06; right: -10px; top: -10px; }
  .sh-cert-card h4 { font-size: 14px; font-weight: 700; margin-bottom: 6px; position: relative; }
  .sh-cert-card p { font-size: 12px; opacity: 0.85; line-height: 1.4; margin-bottom: 14px; position: relative; }
  .sh-history-title { font-size: 14px; font-weight: 700; color: var(--marron); margin-bottom: 12px; }
  .sh-history-list { display: flex; flex-direction: column; gap: 8px; }
  .sh-history-item { background: white; border-radius: 12px; padding: 14px 16px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 1px 6px rgba(0,0,0,0.03); }
  .sh-history-item .info h5 { font-size: 12px; font-weight: 700; color: var(--marron); margin-bottom: 2px; }
  .sh-history-item .info span { font-size: 11px; color: var(--gris); }
  .sh-badge-green { background: rgba(76,175,80,0.12); color: #2E7D32; font-size: 10px; font-weight: 700; padding: 4px 10px; border-radius: 8px; }
  .sh-badge-blue { background: rgba(33,150,243,0.12); color: #1565C0; font-size: 10px; font-weight: 700; padding: 4px 10px; border-radius: 8px; }

  /* === ALIADOS === */
  .sh-aliados-list { display: flex; flex-direction: column; gap: 12px; }
  .sh-aliado-card { background: white; border-radius: 16px; padding: 16px; display: flex; gap: 14px; align-items: flex-start; box-shadow: 0 2px 10px rgba(0,0,0,0.04); }
  .sh-aliado-avatar { width: 50px; height: 50px; background: var(--beige); border-radius: 14px; display: flex; align-items: center; justify-content: center; font-size: 24px; flex-shrink: 0; }
  .sh-aliado-info h4 { font-size: 14px; font-weight: 700; color: var(--marron); margin-bottom: 2px; }
  .sh-aliado-info p { font-size: 12px; color: var(--gris); line-height: 1.4; }
  .sh-aliado-info .tag { display: inline-block; background: var(--verde-claro); color: var(--verde-oscuro); padding: 2px 8px; border-radius: 6px; font-size: 10px; font-weight: 700; margin-top: 6px; }

  /* === CHAT === */
  .sh-chat-header { background: var(--verde); padding: 16px 20px; display: flex; align-items: center; gap: 12px; border-bottom: 3px solid var(--dorado); flex-shrink: 0; }
  .sh-chat-avatar { width: 40px; height: 40px; background: var(--blanco); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 20px; border: 2px solid var(--dorado); }
  .sh-chat-info h3 { margin: 0; color: white; font-size: 15px; font-weight: 800; }
  .sh-chat-info p { margin: 2px 0 0 0; color: #E8DCC4; font-size: 11px; font-weight: 600; }
  .sh-chat-messages { flex: 1; overflow-y: auto; padding: 16px; display: flex; flex-direction: column; gap: 10px; }
  .sh-message { max-width: 85%; padding: 10px 14px; border-radius: 14px; font-size: 13px; line-height: 1.5; animation: fadeIn 0.3s ease; }
  .sh-message-bot { background: white; color: var(--marron); align-self: flex-start; border-bottom-left-radius: 4px; box-shadow: 0 2px 8px rgba(0,0,0,0.06); border-left: 3px solid var(--verde); }
  .sh-message-user { background: var(--marron); color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
  .sh-message-bot strong { color: var(--verde); }
  .sh-typing { display: flex; gap: 4px; padding: 12px 14px; background: white; border-radius: 14px; border-bottom-left-radius: 4px; align-self: flex-start; box-shadow: 0 2px 8px rgba(0,0,0,0.06); width: 56px; }
  .sh-typing-dot { width: 8px; height: 8px; background: var(--verde); border-radius: 50%; animation: typingBounce 1.4s infinite ease-in-out both; }
  .sh-typing-dot:nth-child(1) { animation-delay: -0.32s; }
  .sh-typing-dot:nth-child(2) { animation-delay: -0.16s; }
  @keyframes typingBounce { 0%, 80%, 100% { transform: scale(0.6); opacity: 0.4; } 40% { transform: scale(1); opacity: 1; } }
  .sh-chat-input-area { padding: 10px 16px 16px; background: white; border-top: 1px solid var(--beige); display: flex; gap: 10px; align-items: center; flex-shrink: 0; }
  .sh-chat-input { flex: 1; border: 2px solid var(--beige); border-radius: 24px; padding: 10px 14px; font-family: 'Montserrat', sans-serif; font-size: 13px; background: var(--crema); color: var(--marron); outline: none; }
  .sh-chat-input:focus { border-color: var(--verde); }
  .sh-send-btn { width: 38px; height: 38px; border-radius: 50%; background: var(--verde); border: none; color: white; font-size: 14px; cursor: pointer; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
  .sh-chat-quick { display: flex; flex-wrap: wrap; gap: 6px; padding: 0 16px 10px; flex-shrink: 0; }
  .sh-chat-quick-btn { background: var(--beige); border: 1px solid var(--verde); color: var(--marron); padding: 5px 10px; border-radius: 14px; font-size: 11px; font-weight: 600; cursor: pointer; font-family: 'Montserrat', sans-serif; }

  /* === INVERSOR === */
  .sh-invest-card { background: white; border-radius: 16px; padding: 20px; margin-bottom: 16px; box-shadow: 0 2px 10px rgba(0,0,0,0.04); }
  .sh-invest-card h4 { font-size: 13px; font-weight: 700; color: var(--marron); text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 12px; }
  .sh-metric-row { display: flex; justify-content: space-between; align-items: center; padding: 10px 0; border-bottom: 1px solid var(--beige); }
  .sh-metric-row:last-child { border-bottom: none; }
  .sh-metric-row .label { font-size: 13px; color: var(--gris); }
  .sh-metric-row .value { font-size: 16px; font-weight: 700; color: var(--marron); }
  .sh-metric-row .value.positive { color: #2E7D32; }
  .sh-metric-row .value.negative { color: var(--rojo); }
  .sh-chart-placeholder { background: var(--beige); border-radius: 12px; padding: 40px 20px; text-align: center; color: var(--gris); font-size: 13px; }
  .sh-growth-bar { height: 8px; background: var(--beige); border-radius: 4px; overflow: hidden; margin-top: 6px; }
  .sh-growth-fill { height: 100%; background: var(--verde); border-radius: 4px; transition: width 0.5s ease; }

  /* === PERFIL === */
  .sh-profile-header { background: var(--verde); padding: 32px 24px; text-align: center; color: white; }
  .sh-profile-avatar { width: 80px; height: 80px; background: rgba(255,255,255,0.2); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 40px; margin: 0 auto 12px; border: 3px solid var(--dorado); }
  .sh-profile-header h3 { font-size: 20px; font-weight: 800; }
  .sh-profile-header p { font-size: 13px; opacity: 0.9; margin-top: 4px; }
  .sh-profile-body { padding: 20px; }
  .sh-profile-menu { display: flex; flex-direction: column; gap: 8px; }
  .sh-menu-item { background: white; border-radius: 14px; padding: 16px; display: flex; align-items: center; gap: 14px; box-shadow: 0 2px 8px rgba(0,0,0,0.04); cursor: pointer; transition: all 0.2s; }
  .sh-menu-item:hover { transform: translateX(4px); }
  .sh-menu-icon { width: 40px; height: 40px; background: var(--beige); border-radius: 12px; display: flex; align-items: center; justify-content: center; font-size: 18px; }
  .sh-menu-text { flex: 1; }
  .sh-menu-text h4 { font-size: 14px; font-weight: 700; color: var(--marron); }
  .sh-menu-text p { font-size: 12px; color: var(--gris); }
  .sh-menu-arrow { font-size: 18px; color: var
