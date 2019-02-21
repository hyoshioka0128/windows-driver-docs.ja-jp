---
title: マイク配列 Geometry 記述子の形式
description: マイク配列 Geometry 記述子の形式
ms.assetid: 83fae1e2-cc67-4322-8250-f642508383ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99d8b688d21a898ca0b726d5bc3bd0a2a57b2de3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549870"
---
# <a name="microphone-array-geometry-descriptor-format"></a>マイク配列 Geometry 記述子の形式


USB オーディオ マイクの配列が接続されているシステムに自体を記述する必要があります。 つまり、配列デバイス自体で配列を記述するために必要なパラメーターを埋め込む必要があります。 使用して、デバイスから配列のジオメトリの情報を取得、**取得\_MEM**要求。

標準の形式では、USB オーディオ デバイス ジオメトリに関する情報を提供する必要があります。 そのため、Windows Vista の USB オーディオ クラス ドライバーを使用することを意図した USB マイク アレイには、次の表で定義されている情報の形式を使用する記述子を提供する必要があります。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">フィールド</th>
<th align="left">サイズ</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>guidMicArrayID</p></td>
<td align="left"><p>16</p></td>
<td align="left"><p>グローバル一意識別子 (GUID)</p></td>
<td align="left"><p>メモリ ({07FE86C1-8948-4db5-B184-C5162D4AD314}) のマイク配列の情報の開始をマークするための一意の ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16</p></td>
<td align="left"><p>wDescriptorLength</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク配列については、GUID と長さのフィールドなどの長さを (バイト単位)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>wVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>バイナリ コード化された 10 進数 (BCD)</p></td>
<td align="left"><p>この記述子続けてマイク配列の指定のバージョン番号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20</p></td>
<td align="left"><p>wMicArrayType</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>次の値が定義されています。</p>
<p>00:線形。</p>
<p>01:平面。</p>
<p>02:3 次元 (3 D)。</p>
<p>03 FFFF:予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>22</p></td>
<td align="left"><p>wWorkVertAngBeg</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>作業のボリュームの垂直方向の角度の開始。</p></td>
</tr>
<tr class="even">
<td align="left"><p>24</p></td>
<td align="left"><p>wWorkVertAngEnd</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>作業のボリュームの垂直方向の角度の終了。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>26</p></td>
<td align="left"><p>wWorkHorAngBeg</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>作業のボリュームの水平方向の角度の先頭。</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>wWorkHorAngEnd</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>作業のボリュームの水平方向の角度の終了。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>30</p></td>
<td align="left"><p>wWorkFreqBandLo</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>作業の周波数の範囲の下限値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>32</p></td>
<td align="left"><p>wWorkFreqBandHi</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>作業の周波数の範囲の上限値です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>34</p></td>
<td align="left"><p>wNumberOfMics</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>次の個々 のマイク定義の数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>36</p></td>
<td align="left"><p>wMicrophoneType(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク 0 の種類を一意に識別する数値。</p>
<p>00:全方向</p>
<p>01:SubCardioid</p>
<p>02:Cardioid</p>
<p>03:SuperCardioid</p>
<p>04:HyperCardioid</p>
<p>05:8 の形</p>
<p>0F - FF:ベンダー定義</p></td>
</tr>
<tr class="odd">
<td align="left"><p>38</p></td>
<td align="left"><p>wXCoordinate(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク 0 の x 座標。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40</p></td>
<td align="left"><p>wYCoordinate(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク 0 の y 座標。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>42</p></td>
<td align="left"><p>wZCoordinate(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク 0 の z 座標。</p></td>
</tr>
<tr class="even">
<td align="left"><p>44</p></td>
<td align="left"><p>wMicVertAngle(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク 0 のメイン応答軸 (MRA) 垂直方向の角度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>46</p></td>
<td align="left"><p>wMicHorAngle(0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク 0 の MRA 水平方向の角度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>N-2 にマイク定義 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>34+((n-1)<em>12)</p></td>
<td align="left"><p>wMicType(n-1)</p></td>
<td align="left"></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク n-1 の種類を一意に識別する数値。</p>
<p>00:全方向</p>
<p>01:SubCardioid</p>
<p>02:Cardioid</p>
<p>03:SuperCardioid</p>
<p>04:HyperCardioid</p>
<p>05:8 の形</p>
<p>0F - FF:ベンダー定義</p></td>
</tr>
<tr class="even">
<td align="left"><p>36+((n-1)</em>12)</p></td>
<td align="left"><p>wXCoordinate(n-1)</p></td>
<td align="left"></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク n-1 の x 座標。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>38+((n-1)<em>12)</p></td>
<td align="left"><p>wYCoordinate(n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク n-1 の y 座標。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40+((n-1)</em>12)</p></td>
<td align="left"><p>wZCoordinate(n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク n-1 の z 座標。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>42+((n-1)<em>12)</p></td>
<td align="left"><p>wMicVertAngle(n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク n-1 の MRA 垂直方向の角度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>44+((n-1)</em>12)</p></td>
<td align="left"><p>wMicHorAngle(n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>数値</p></td>
<td align="left"><p>マイク n-1 の MRA 水平方向の角度。</p></td>
</tr>
</tbody>
</table>

 

4 要素のマイク配列の記述子でこの情報の形式を使用する方法の詳細な例については、「付録 A を参照してください、[方法の構築および Windows Vista のマイク配列を使用して](https://go.microsoft.com/fwlink/p/?linkid=306613)ホワイト ペーパー。

**注:**  

 

-   バージョン番号をマイク配列の情報に含めるときに、記述子を元の仕様が実装された後に更新することができます。 バージョン番号は、BCD 値です。 たとえば、現在のバージョン (1.0) は 0x0100 として表されます。

-   オフセットとサイズの値では、(バイト単位) です。

-   すべての角度は、1/10000 ラジアン単位で表されます。 たとえば、3.1416 ラジアンは 31416 として表されます。 値の範囲は-31416 から 31416、包括的です。

-   ミリメートル単位では、X、y、z 座標が表されます。 値の範囲は-32767 から 32767 です。

-   印刷の向き、軸、および座標システムの角度の正の方向については、マイク配列のホワイト ペーパー「付録 B を参照してください。

-   頻度の値が Hz で表現されます。 頻度の値の範囲はからフィールドのサイズによってのみ制限されます**wWorkFreqBandLo**に**wWorkFreqBandHi**します。

 

 




