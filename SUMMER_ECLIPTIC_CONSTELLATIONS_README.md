# 夏の黄道付近の3星座を追加しました

統合版のトップページに、**さそり座・いて座・へびつかい座**の主要恒星と、学習用の星座線を追加しました。これらは夏に黄道付近を観察する際に親しみやすい星座です。さそり座といて座は黄道12星座に含まれますが、へびつかい座は黄道付近に位置するものの、一般にいう黄道12星座には含まれません。

> 現在の線は「星座を見つけるための分かりやすい結び方」です。IAUが正式に定義しているのは星座の境界であり、星を結ぶ線の形そのものは公式には一意に決められていません。[1]

## 追加した主要星

| 星座 | 代表星 | アプリ内の役割 |
|---|---|---|
| さそり座 | ジュバ、アクラブ、アンタレス、サルガス、シャウラ、レサト | アンタレスから尾の先へ向かう特徴的な曲線を表示する |
| いて座 | カウス・ボレアリス、カウス・メディア、カウス・アウストラリス、ヌンキ、アスケラ | 南の低い空にある主要星を、単純な「ティーポット」風の形で結ぶ |
| へびつかい座 | ラス・アルハゲ、ケバルライ、イェド・プリオル、イェド・ポステリオル、サビク | 黄道近くにある大きな星座の主要星を、分かりやすい五角形風に結ぶ |

主要星のJ2000赤経・赤緯は、SIMBADの天文学データベースで照合した値を小数表記に変換して使用しています。例えば、アンタレス、カウス・アウストラリス、ラス・アルハゲ、シャウラ、ヌンキ、ケバルライ、イェド・プリオルを確認しました。[2] [3] [4] [5] [6] [7] [8]

## スマホでの確認手順

最初は、以前と同じトップページをAndroid Chromeで開きます。

```text
https://8080-igxd900hhtdau6obo07tc-5f886b00.sg1.manus.computer/
```

| 順番 | 操作 | 見るポイント |
|---:|---|---|
| 1 | `カメラを開始する`、`現在地を取得する`、`スマホの向きを取得する` を順に押す | 方位と位置情報を取得する |
| 2 | `主要な恒星を表示する` を押す | 画面内にある明るい恒星だけに印が出る |
| 3 | プルダウンで `さそり座` を選ぶ | アンタレスが見える南の空へ向け、必要な星が同時に画面内に入ると線が出る |
| 4 | `いて座（主要星）` または `へびつかい座（主要星）` を選ぶ | 同じように、対象の星が画面内にそろったときに線が出る |
| 5 | 必要に応じて `Name` を押す | 天体名を重ねて確認できる |

星座線は、必要な代表星が**すべて**画面内に入ったときだけ描画します。線が見えない場合は不具合とは限らず、対象の星の一部が地平線下・高度10°以下・カメラ画面外にある可能性があります。スマホを横向きにすると、縦長より広い空を一度に写しやすくなります。

日本の多くの地域では、夏の南の空でさそり座といて座が比較的低い位置になります。見通しがよく、南側に建物や山が少ない場所で試してください。

## ブラウザでの検証

更新後のページには、3つの新しいプルダウン選択肢が表示されることを確認しました。さらに東京付近のテスト位置・時刻・端末姿勢を与え、`さそり座`、`いて座（主要星）`、`へびつかい座（主要星）` を順に選択して座標変換と星座線の描画判定を実行しました。3種類とも計算エラーは発生しませんでした。テスト時のカメラ方向では対象星が画面に入らなかったため、線の表示待ちとなる結果は正常です。

## 参考資料

[1]: https://iau.org/public/themes/constellations/ "IAU: The Constellations"
[2]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Antares&output.format=ASCII "SIMBAD: Antares"
[3]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Kaus+Australis&output.format=ASCII "SIMBAD: Kaus Australis"
[4]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Rasalhague&output.format=ASCII "SIMBAD: Rasalhague"
[5]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Shaula&output.format=ASCII "SIMBAD: Shaula"
[6]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Nunki&output.format=ASCII "SIMBAD: Nunki"
[7]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Cebalrai&output.format=ASCII "SIMBAD: Cebalrai"
[8]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Yed+Prior&output.format=ASCII "SIMBAD: Yed Prior"
