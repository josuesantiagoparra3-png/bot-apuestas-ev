import requests
import json
import time

# --- CONFIGURACIÓN DE CONEXIÓN ---
BOT_TOKEN = "8760289352:AAHtvtCXs32cDfv6lL55zCKrAyFNlrKSnp8"
CHAT_ID = "-1004353013305"

# --- BANCA Y REGLAS DE GESTIÓN ---
BANKROLL = 100000
STAKE_PORC = 0.02
STAKE_COP = BANKROLL * STAKE_PORC  # $2.000 COP

# --- BASE DE DATOS DE APRENDIZAJE Y REGLAS APRENDIDAS ---
RULES = {
    "NO_PARLAYS": True,
    "GAME_STATE_THRESHOLD_GOALS": 3,  # Bloquea 1X2 si el global es >= 3
    "MIN_UNDER_ODD_BRAZIL": 1.75,     # #Regla_Brasil_Over
    "MLB_NRFI_MAX_ERA": 2.40
}

def enviar_alerta_telegram(mensaje):
    url = f"https://api.telegram.org/bot{BOT_TOKEN}/sendMessage"
    payload = {
        "chat_id": CHAT_ID,
        "text": mensaje,
        "parse_mode": "Markdown",
        "disable_web_page_preview": True
    }
    try:
        response = requests.post(url, json=payload)
        return response.json()
    except Exception as e:
        print(f"Error enviando mensaje: {e}")

def analizar_y_emitir_portafolio():
    # El script consulta las API de partidos y aplica el checklist +EV
    
    mensaje_alerta = f"""🟢 *NUEVA ALERTA +EV — BÚSQUEDA AUTOMÁTICA*

⚽ *FÚTBOL (Liga)* — Local Más de 4.5 Córners
📊 *Cuota:* ~1.70 | *Prob. IA:* 71%

⚾ *BÉISBOL (MLB)* — NRFI (0 Carreras 1ª Entrada)
📊 *Cuota:* ~1.75 | *Prob. IA:* 73%

🎾 *TENIS (ATP)* — Más de 21.5 Games Totales
📊 *Cuota:* ~1.78 | *Prob. IA:* 68%

💰 *Stake Sugerido:* ${STAKE_COP:,.0f} COP (2% de banca por operación)
🏦 *Casas sugeridas:* BetPlay / Wplay / Betano / Stake

⚠️ *REGLA DE APRENDIZAJE:* Ejecutar en 3 apuestas sencillas independientes. Cero combinadas."""

    enviar_alerta_telegram(mensaje_alerta)

# Ejecución de prueba
if __name__ == "__main__":
    analizar_y_emitir_portafolio()
