# 『無線静電容量無接点キーボードを作ってみた』LTspice補足資料

第1章に登場する5本のネットリストです。本文の図と見比べながら、回路定数や観測点を変えて試せます。

| ファイル | 本文で確かめたこと | 波形・ログで見るところ |
| --- | --- | --- |
| [pulldown.cir](ec-components/pulldown.cir) | プルダウン抵抗による電位の戻りと、漏れ電流によるずれ | 抵抗の有無で検知点がどのように変わるか |
| [discharge.cir](ec-components/discharge.cir) | 放電経路の抵抗によるピーク電流と放電時間の違い | スイッチが閉じた直後の電流と、検知点の残留電圧 |
| [drive.cir](ec-components/drive.cir) | 駆動側の直列抵抗によるリンギングの抑制 | 仮定した配線の末端の電圧 |
| [input.cir](ec-components/input.cir) | 入力の直列抵抗によるクランプ電流の制限 | 入力保護に流れ込む電流 |
| [scan.cir](ec-single-key/scan.cir) | 1キーの充電・増幅・放電。未押下1 pFと押下2 pFを比較 | `V(sense_1pf)`／`V(sense_2pf)`、`V(out_1pf)`／`V(out_2pf)`、充電開始の約5 µs後の出力 |

## 実行する

1. [Analog Devicesの配布ページ](https://www.analog.com/en/resources/design-tools-and-calculators/ltspice-simulator.html)からLTspiceをインストールします。
2. GitHubの **Code → Download ZIP** で取得して展開し、試したい `.cir` をLTspiceで開いて **Run** を選びます。
3. 波形画面の **Add Trace** で信号を追加します。測定時刻・ピークなど、ネットリスト末尾の `.meas` で指定した数値は **SPICE Error Log** に出ます。
4. `scan.cir` の `UniversalOpAmp2.lib` が見つからない場合は、インストールしたLTspiceの `lib/sub` にある同名ファイルを、手元の `scan.cir` と同じフォルダーへコピーします。

各モデルは抵抗の役割や容量差を見やすくするために条件を絞ったものです。たとえば `drive.cir` の100 pFは配線と負荷をまとめた仮定値で、キーの容量は `scan.cir` で1 pFと2 pFに設定しています。`scan.cir` では付属の汎用オペアンプモデルを参照します。実機のADCやIC固有の挙動を再現する場合は、別途そのモデルや条件が必要です。

独自のネットリストの利用条件は [LICENSE](LICENSE) を参照してください。LTspice本体と付属ライブラリはAnalog Devicesの配布物を利用します。
