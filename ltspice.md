# 第1章のシミュレーションを再現する

本文で使った5本のネットリストです。波形の数値は、部品の役割を比べるために置いた条件での計算例です。

| ネットリスト | 重ねて表示する信号 | 誌面と見比べるところ |
| --- | --- | --- |
| [pulldown.cir](ec-components/pulldown.cir) | `V(hold_none)`／`V(hold_pd)`、`V(leak_none)`／`V(leak_pd)` | 立ち上がり終了から10 µs後、検知点は約29.7 mV／18.9 mV。漏れ電流を加えた別の枝では、1 ms後に約4.50 mV／0.100 mV。 |
| [discharge.cir](ec-components/discharge.cir) | `I(VPROBE_none)`／`I(VPROBE_rd)`、`V(hold_none)`／`V(hold_rd)` | 放電電流のピークは約5.99 mA／0.146 mA。スイッチが閉じて50 ns後の検知点は約0 mV／9.97 mV。 |
| [drive.cir](ec-components/drive.cir) | `V(end_none)`／`V(end_rd)` | 配線末端のピークが約4.44 V／3.30 Vになるところ。 |
| [input.cir](ec-components/input.cir) | `I(VPROBE_none)`／`I(VPROBE_ri)` | 立ち上がりのピークは約23.5 mA／2.13 mA。1.5 µs時点では約23.5 mA／1.14 mA。 |
| [scan.cir](ec-single-key/scan.cir) | `V(sense_1pf)`／`V(sense_2pf)`、`V(out_1pf)`／`V(out_2pf)` | 未押下1 pF／押下2 pFを比較。10 µs時点の出力は約0.59 V／1.18 V。 |

抵抗を比較する4例では、左が抵抗なし、右が抵抗ありです。電圧と電流は別々のグラフ枠に分けると、縦軸を読みやすくなります。

## 実行する

1. [Analog Devicesの配布ページ](https://www.analog.com/en/resources/design-tools-and-calculators/ltspice-simulator.html)からLTspiceをインストールします。
2. [リポジトリのトップ](README.md)で **Code → Download ZIP** を選びます。展開したファイルから試したい `.cir` を開き、**Run** を選びます。
3. 波形画面の **Add Trace** で、表にある信号を追加します。測定時刻やピークの値は、ネットリスト末尾の `.meas` の名前を手がかりに **SPICE Error Log** で確認できます。
4. `scan.cir` の `UniversalOpAmp2.lib` が見つからない場合は、インストールしたLTspiceの `lib/sub` にある同名ファイルを、手元の `scan.cir` と同じフォルダーへコピーします。

`drive.cir` の100 pFは、配線と負荷をまとめた仮定値です。キーの静電容量を変える実験は `scan.cir` で試せます。`scan.cir` の増幅器にはLTspice付属の汎用モデルを使います。

独自のネットリストの利用条件は [LICENSE](LICENSE) を参照してください。LTspice本体と付属ライブラリはAnalog Devicesの配布物を利用します。
