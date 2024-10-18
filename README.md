# mezuniyet-kodu



pip install Flask



from flask import Flask, render_template, request
import random

app = Flask(__name__)

# Oyun veritabanı
oyunlar = {
    "Aksiyon": {
        "Kolay": ["GTA5", "Limbo"],
        "Orta": ["Valorant", "Pubg Mobile"],
        "Zor": ["Fortnite", "CS GO"]
    },
    "RPG": {
        "Kolay": ["Metin 2", "Undertale"],
        "Orta": ["The Witcher 3: Wild Hunt", "Persona 5"],
        "Zor": ["Darkest Dungeon", "Divinity: Original Sin 2"]
    },
    "Spor": {
        "Kolay": ["UFLl", "Braid"],
        "Orta": ["Efootball", "Topspin 2K25
"],
        "Zor": ["Fifa 25", "NBA 2K25"]
    },
    "Strateji": {
        "Kolay": ["Civilization VI", "Cities: Skylines"],
        "Orta": ["StarCraft II", "Leauge Of Legends"],
        "Zor": ["Crusader Kings III", "Europa Universalis IV"]
    }
}

@app.route('/')
def ana_sayfa():
    return render_template('index.html')

@app.route('/oneri', methods=['POST'])
def oyun_oner():
    tur = request.form['tur']
    zorluk = request.form['zorluk']
    
    if tur in oyunlar and zorluk in oyunlar[tur]:
        oyun = random.choice(oyunlar[tur][zorluk])
        return render_template('sonuc.html', oyun=oyun)
    else:
        return "Geçersiz tür veya zorluk seviyesi!"

if __name__ == '__main__':
    app.run(debug=True)
