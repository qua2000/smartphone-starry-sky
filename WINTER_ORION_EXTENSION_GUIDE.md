# 冬の主要星・オリオン座をAR表示へ追加する方法

このガイドでは、すでに作成した `major-stars-ar-sample.html` を土台に、**冬の主要な星を点で表示する段階**と、**オリオン座・冬の大三角を線で表示する段階**に分けて説明します。新しいカメラ処理、位置情報処理、端末姿勢処理、天文計算は不要です。すでにある仕組みを再利用し、星表のデータと「どの星を線で結ぶか」という定義を追加します。

> **大切な進め方**：最初から全部の星座線を描かず、(1) ベテルギウス1個、(2) オリオン座の7星を点で表示、(3) オリオンの三つ星、(4) 全体の線、という順で実機確認してください。一度に変更する量を小さくすると、間違いが起きても原因を見つけやすくなります。

## 0. 作業用のコピーを作る

最初に、`major-stars-ar-sample.html` を複製して `winter-orion-ar-sample.html` という名前にしてください。元の夏の大三角サンプルを残せるため、安心して変更できます。

```bash
cp major-stars-ar-sample.html winter-orion-ar-sample.html
```

GitHubのWeb画面だけで作業する場合は、`major-stars-ar-sample.html` を開き、内容をコピーして、`winter-orion-ar-sample.html` という新しいファイルとして保存します。

## 1. まず冬の星を「点」として追加する

`winter-orion-ar-sample.html` の `BRIGHT_STARS` 配列を探してください。この配列には、すでにシリウス、ベガなどのデータが入っています。最後の `]` の直前に、次の8件を追加します。先頭の `{` の前にある既存データの閉じ `}` のあとへ、**カンマ `,`** を入れることを忘れないでください。

```js
// オリオン座の両肩。ベテルギウスは赤みを付けて表示します。
{
  id: "betelgeuse",
  nameJa: "ベテルギウス",
  nameEn: "Betelgeuse",
  raHoursJ2000: 5.919529266666,
  decDegJ2000: 7.407064000000,
  magnitude: 0.42,
  color: "#ffb08c",
  markerSize: 15
},
{
  id: "bellatrix",
  nameJa: "ベラトリックス",
  nameEn: "Bellatrix",
  raHoursJ2000: 5.418850902777,
  decDegJ2000: 6.349703277777,
  magnitude: 1.64,
  color: "#dbe8ff",
  markerSize: 11
},

// オリオンの三つ星。西からアルニタク、アルニラム、ミンタカです。
{
  id: "alnitak",
  nameJa: "アルニタク",
  nameEn: "Alnitak",
  raHoursJ2000: 5.679312961110,
  decDegJ2000: -1.942573583333,
  magnitude: 1.77,
  color: "#d8e7ff",
  markerSize: 10
},
{
  id: "alnilam",
  nameJa: "アルニラム",
  nameEn: "Alnilam",
  raHoursJ2000: 5.603559263888,
  decDegJ2000: -1.201919138888,
  magnitude: 1.69,
  color: "#d8e7ff",
  markerSize: 10
},
{
  id: "mintaka",
  nameJa: "ミンタカ",
  nameEn: "Mintaka",
  raHoursJ2000: 5.533444469444,
  decDegJ2000: -0.299095111110,
  magnitude: 2.41,
  color: "#d8e7ff",
  markerSize: 9
},

// オリオン座の両足。リゲルは特に明るいので少し大きくします。
{
  id: "rigel",
  nameJa: "リゲル",
  nameEn: "Rigel",
  raHoursJ2000: 5.242297805555,
  decDegJ2000: -8.201638361111,
  magnitude: 0.13,
  color: "#d6eaff",
  markerSize: 15
},
{
  id: "saiph",
  nameJa: "サイフ",
  nameEn: "Saiph",
  raHoursJ2000: 5.795941344555,
  decDegJ2000: -9.669604918610,
  magnitude: 2.06,
  color: "#d8e7ff",
  markerSize: 10
},

// シリウスとベテルギウスと結んで、冬の大三角を作る星です。
{
  id: "procyon",
  nameJa: "プロキオン",
  nameEn: "Procyon",
  raHoursJ2000: 7.655033194444,
  decDegJ2000: 5.224987555554,
  magnitude: 0.37,
  color: "#fff2c9",
  markerSize: 14
}
```

この段階では、既存の `SUMMER_TRIANGLE`、`drawSummerTriangle()`、ボタンのコードは触りません。既存の `主要な一等星を表示する` を押すと、季節・時刻・スマホを向けた方向に応じて、追加した冬の星も画面内に出ます。

| 追加する星 | オリオン座内の役割 | 見かけのV等級 | まず確認したいこと |
|---|---|---:|---|
| ベテルギウス | 左肩 | 0.42 | 赤みのある大きめの点が出る |
| ベラトリックス | 右肩 | 1.64 | ベテルギウスと対になる点が出る |
| アルニタク、アルニラム、ミンタカ | 三つ星 | 1.77、1.69、2.41 | 近い3点が並ぶ |
| リゲル、サイフ | 両足 | 0.13、2.06 | 三つ星の下側に位置する |
| プロキオン | 冬の大三角の頂点 | 0.37 | シリウスとは別の明るい点が出る |

データはSIMBADのICRS/J2000座標・V等級を小数値へ変換して使用しています。[1] [2] [3]

## 2. 三つ星だけを最初に線で結ぶ

点の表示が確認できたら、次にオリオンの三つ星だけを線で結びます。`SUMMER_TRIANGLE` 定義のすぐ下へ、次の定義を追加してください。

```js
const ORION_BELT = {
  nameJa: "オリオンの三つ星",
  starIds: ["alnitak", "alnilam", "mintaka"],
  edges: [
    ["alnitak", "alnilam"],
    ["alnilam", "mintaka"]
  ]
};
```

続いて、`drawSummerTriangle()` の内容を丸ごと次の汎用関数に置き換えます。これは、引数 `pattern` に渡した星の並びを描く関数です。夏の大三角、三つ星、オリオン座全体のどれにも使えます。

```js
function drawPattern(pattern) {
  const width = cameraArea.clientWidth;
  const height = cameraArea.clientHeight;
  constellationContext.clearRect(0, 0, width, height);

  // 線を結ぶ全ての星が画面内にない場合は、何も描かないようにします。
  const points = pattern.starIds.map((id) => projectedStars.get(id));
  if (points.some((point) => point === undefined)) {
    triangleStateValue.textContent = `${pattern.nameJa}：必要な星が画面内にそろうと表示`;
    return;
  }

  constellationContext.save();
  constellationContext.strokeStyle = "rgba(170, 217, 255, 0.88)";
  constellationContext.lineWidth = 2;
  constellationContext.setLineDash([7, 5]);
  constellationContext.shadowColor = "rgba(169, 216, 255, 0.72)";
  constellationContext.shadowBlur = 8;
  constellationContext.beginPath();

  for (const [fromId, toId] of pattern.edges) {
    const from = projectedStars.get(fromId);
    const to = projectedStars.get(toId);
    constellationContext.moveTo(from.screen.xPercent * width / 100, from.screen.yPercent * height / 100);
    constellationContext.lineTo(to.screen.xPercent * width / 100, to.screen.yPercent * height / 100);
  }

  constellationContext.stroke();
  constellationContext.restore();
  triangleStateValue.textContent = `${pattern.nameJa}を表示中`;
}
```

`updateSkyOverlay()` の中にある `drawSummerTriangle();` は、試しに次の1行へ変更してください。

```js
drawPattern(ORION_BELT);
```

これで、三つの星が画面内に同時に入った時だけ、二本の線が表示されます。ここまで動けば、星座線を描く最も大切な仕組みを理解できています。

## 3. オリオン座全体の線を追加する

三つ星の確認後、同じ場所に次の `ORION` 定義を追加してください。これは教育用の分かりやすい「砂時計型」の線です。IAUが公式に定めるものは星座の境界であり、線の結び方自体はアプリの表示ルールとして決めます。[4]

```js
const ORION = {
  nameJa: "オリオン座",
  starIds: [
    "betelgeuse", "bellatrix",
    "alnitak", "alnilam", "mintaka",
    "rigel", "saiph"
  ],
  edges: [
    ["betelgeuse", "bellatrix"],  // 両肩
    ["betelgeuse", "alnitak"],    // 左肩から三つ星へ
    ["bellatrix", "mintaka"],     // 右肩から三つ星へ
    ["alnitak", "alnilam"],       // 三つ星 1本目
    ["alnilam", "mintaka"],       // 三つ星 2本目
    ["alnitak", "saiph"],         // 左側の脚
    ["mintaka", "rigel"],         // 右側の脚
    ["saiph", "rigel"]            // 両足
  ]
};
```

そして、先ほどの1行を次のように変更します。

```js
drawPattern(ORION);
```

| 表示段階 | `drawPattern()` に渡すもの | 期待する線 |
|---|---|---|
| 最初の線 | `ORION_BELT` | 三つ星を結ぶ2本の線 |
| オリオン座全体 | `ORION` | 両肩・三つ星・両脚を結ぶ線 |
| 元の夏の大三角 | `SUMMER_TRIANGLE` | ベガ・アルタイル・デネブの三角形 |

**注意**：オリオン座全体が同時に画面内へ入らなければ、線が表示されないのは正常です。スマホを横向きにして画角を広くし、空の中ほどを向くと試しやすくなります。

## 4. 冬の大三角を追加する

冬の大三角は、シリウス・ベテルギウス・プロキオンを結ぶ星の並びです。次の定義を追加すれば、夏の大三角とまったく同じ方法で扱えます。

```js
const WINTER_TRIANGLE = {
  nameJa: "冬の大三角",
  starIds: ["sirius", "betelgeuse", "procyon"],
  edges: [
    ["sirius", "betelgeuse"],
    ["betelgeuse", "procyon"],
    ["procyon", "sirius"]
  ]
};
```

`drawPattern(WINTER_TRIANGLE);` と書けば、冬の大三角を描きます。実用版では、現在は `drawPattern(ORION)` と直接決め打ちしている部分を、ボタンによって切り替えられるようにします。

```js
let selectedPattern = ORION;

function selectPattern(pattern) {
  selectedPattern = pattern;
  updateSkyOverlay();
}

// 例：ボタンを押したときに選ぶ星の並びを変更します。
selectPattern(WINTER_TRIANGLE);
// selectPattern(ORION);
// selectPattern(SUMMER_TRIANGLE);
```

## 5. 最初の実機確認の順番

| 確認する順番 | 画面で行うこと | 成功の目安 |
|---|---|---|
| 1 | 追加した星データだけで点を表示する | 冬の夜に、ベテルギウスやリゲルなどの点が出る |
| 2 | `ORION_BELT` の2本線を表示する | 三つ星に対応する3点を2本の線が結ぶ |
| 3 | `ORION` の全体線を表示する | 砂時計型に近い輪郭が現れる |
| 4 | `WINTER_TRIANGLE` を表示する | シリウス・ベテルギウス・プロキオンが三角形に結ばれる |
| 5 | 夏の大三角へ戻す | 既存機能が変わらず動く |

冬の星座は、日本付近では冬の夜に確認しやすくなりますが、月と同じく、日時・現在地・向けている方角によって画面内に現れる星が変わります。実際の星とマーカーの位置が少しずれる場合は、これまでに確認した方位センサーとカメラ画角の誤差が主な原因です。星の追加を一通り確認した後に、明るい星に合わせる**校正機能**を加えると、全体の線もまとめて合わせやすくなります。

## 参考資料

[1]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Betelgeuse&output.format=ASCII "SIMBAD: Betelgeuse"
[2]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Rigel&output.format=ASCII "SIMBAD: Rigel"
[3]: https://simbad.cds.unistra.fr/simbad/sim-id?Ident=NAME+Procyon&output.format=ASCII "SIMBAD: Procyon"
[4]: https://iauarchive.eso.org/public/themes/constellations/ "International Astronomical Union: The Constellations"
