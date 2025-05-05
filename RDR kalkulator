import math
import streamlit as st

def rulett_kalkulator(kiindulopont, korok_szama, kor_ido=6.85):
    """
    Rulett golyó pozíciópredikció kalkulátor
    :param kiindulopont: kezdő mező (0–36)
    :param korok_szama: mennyi teljes kört tesz meg a labda (pl. 15.7)
    :param kor_ido: a kerék egy teljes körének ideje másodpercben (default: 6.85)
    :return: 5 legvalószínűbb mező száma, első az 100%-os
    """

    rulett_sorrend = [
        0, 32, 15, 19, 4, 21, 2, 25, 17, 34, 6, 27, 13, 36, 11, 30, 8,
        23, 10, 5, 24, 16, 33, 1, 20, 14, 31, 9, 22, 18, 29, 7, 28,
        12, 35, 3, 26
    ]

    n = len(rulett_sorrend)
    elmozdulas = int((korok_szama % 1) * n)

    try:
        kiindulo_index = rulett_sorrend.index(kiindulopont)
    except ValueError:
        raise ValueError("Érvénytelen kiindulópont: csak 0–36 lehet, és a számnak szerepelnie kell a keréken.")

    biztonsagos_pozicio = (kiindulo_index + elmozdulas) % n

    lehetseges_indexek = [
        (biztonsagos_pozicio + i) % n for i in [-2, -1, 0, 1, 2]
    ]

    eredmenyek = [rulett_sorrend[i] for i in lehetseges_indexek]
    return list(dict.fromkeys(eredmenyek))

# -------------------------------
# Streamlit UI kezdete
# -------------------------------
st.title("Rulett Predikció Kalkulátor")

kiindulo = st.number_input("Add meg a kiinduló mezőt (0–36):", min_value=0, max_value=36, value=22)
korok = st.number_input("Add meg a labda által megtett körök számát:", min_value=0.0, max_value=50.0, value=15.7, step=0.1)

if st.button("Számítás indítása"):
    try:
        top_5_szam = rulett_kalkulator(kiindulo, korok)
        st.success(f"Top 5 valószínű pozíció: {top_5_szam}")
    except Exception as e:
        st.error(str(e))
