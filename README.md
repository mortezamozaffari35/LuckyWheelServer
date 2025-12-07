from flask import Flask, request, jsonify
import json

app = Flask(__name__)

@app.route('/save_result', methods=['POST'])
def save_result():
    data = request.json
    user_id = data.get('user_id')
    prize = data.get('prize')

    try:
        with open('results.json', 'r', encoding='utf-8') as f:
            results = json.load(f)
    except FileNotFoundError:
        results = []

    results.append({'user_id': user_id, 'prize': prize})

    with open('results.json', 'w', encoding='utf-8') as f:
        json.dump(results, f, ensure_ascii=False, indent=2)

    return jsonify({'status': 'ok', 'message': 'نتیجه ثبت شد!'})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
# LuckyWheelServer
