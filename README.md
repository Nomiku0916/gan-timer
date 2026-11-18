# GANタイマー (gan-timer)

GAN 356 i Carry E（Gen2プロトコル）のための、Android Chrome向けWeb Bluetoothタイマーです。
単一HTMLファイル（`index.html`）で動作します。

## 使い方

1. このページをHTTPS（GitHub Pagesなど）またはlocalhostで開く
2. CubeStationなど他のアプリとの接続を切ってから「キューブに接続」
3. スクランブル（白が上・緑が手前）に合わせてキューブを回す
4. スクランブルが一致すると計測待機になり、最初の一手で計測開始、完成で自動停止

## 機能

- CFOPフェーズ分割: Cross / F2Lスロット×4（完了順）/ OLL（2Look時はEOLL+COLL分割）/ PLL / AUF、手数・TPS
- キューブ内蔵時計のズレを線形フィットで補正（csTimer方式）
- Ao5 / Ao12 / Ao50 / Ao100、ベスト記録
- 履歴はブラウザのlocalStorageに保存。JSONバックアップのエクスポート/インポート対応
- キューブなしで試せるデモモード付き

## 接続について

- GANキューブの暗号化にはMACアドレスが必要です。自動取得できない場合は画面の案内に従って入力してください
- 自動取得を安定させるには Chrome の `chrome://flags/#enable-experimental-web-platform-features` を有効化してください
- 接続ライブラリ [gan-web-bluetooth](https://github.com/afedotov/gan-web-bluetooth)（MIT）をCDNから読み込んでいます

## 開発

ソースは `src/`（cube-core.js: キューブエンジンとCFOP判定、app.js: アプリ本体）にあり、
`python3 build.py` で単一の `index.html` に結合します。`node test/test-core.js` と
`node test/test-app.js` で自動テストが実行できます。
