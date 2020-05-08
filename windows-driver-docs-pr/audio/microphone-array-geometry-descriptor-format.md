---
title: マイク配列ジオメトリ記述子の形式
description: マイク配列ジオメトリ記述子の形式
ms.assetid: 83fae1e2-cc67-4322-8250-f642508383ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44385111ec6915d66e18a78358fe1ae365e12e6e
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925547"
---
# <a name="microphone-array-geometry-descriptor-format"></a>マイク配列ジオメトリ記述子の形式

USB オーディオマイク配列は、それが接続されているシステムについて記述する必要があります。 これは、配列を記述するために必要なパラメーターが配列デバイス自体に埋め込まれている必要があることを意味します。 配列のジオメトリ情報は、 **GET\_MEM**要求を使用してデバイスから取得されます。

USB オーディオデバイスのジオメトリに関する情報は、標準の形式で指定する必要があります。 そのため、Windows Vista USB オーディオクラスドライバーを操作するための USB マイク配列は、次の表に定義されている情報形式を使用する記述子を提供する必要があります。

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
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>guidMicArrayID</p></td>
<td align="left"><p>16</p></td>
<td align="left"><p>グローバル一意識別子 (GUID)</p></td>
<td align="left"><p>メモリ内のマイク配列情報の先頭を示す一意の ID ({07FE86C1-8948-4db5-B184-C5162D4AD314})。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16</p></td>
<td align="left"><p>W記述子の長さ</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク配列情報の長さ (バイト単位)。 GUID フィールドと長さフィールドを含みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>wVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>バイナリのコード化された10進数 (BCD)</p></td>
<td align="left"><p>マイク配列仕様のバージョン番号、その後ろにこの記述子を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20</p></td>
<td align="left"><p>wMicArrayType</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>次の値が定義されています。</p>
<p>00: 線形。</p>
<p>01: 平面。</p>
<p>02: 3-次元 (3D)。</p>
<p>03-FFFF: 予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>22</p></td>
<td align="left"><p>wWorkVertAngBeg</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>ワークボリュームの垂直方向の開始。</p></td>
</tr>
<tr class="even">
<td align="left"><p>24</p></td>
<td align="left"><p>Wworkspace Vertangend</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>作業ボリュームの垂直方向の終了。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>26</p></td>
<td align="left"><p>wWorkHorAngBeg</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>ワークボリュームの水平方向の開始位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>wWorkHorAngEnd</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>作業ボリュームの水平方向の角度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>30</p></td>
<td align="left"><p>W職場 Freqバンド Lo</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>作業周波数の範囲の下限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>32</p></td>
<td align="left"><p>W職場 Freqバンドこんにちは</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>作業周波数の範囲の上限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>34</p></td>
<td align="left"><p>wNumberOfMics</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>次に続く個々のマイク定義の数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>36</p></td>
<td align="left"><p>wMicrophoneType (0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク0の種類を一意に識別する番号。</p>
<p>00: 双方向</p>
<p>01: SubCardioid</p>
<p>02: cardioid</p>
<p>03: SuperCardioid</p>
<p>04: HyperCardioid</p>
<p>05: 8 整形</p>
<p>0F-FF: ベンダーが定義済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>38</p></td>
<td align="left"><p>wXCoordinate (0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク0の x 座標。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40</p></td>
<td align="left"><p>wYCoordinate (0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク0の y 座標。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>42</p></td>
<td align="left"><p>wZCoordinate (0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク0の z 座標。</p></td>
</tr>
<tr class="even">
<td align="left"><p>44</p></td>
<td align="left"><p>wMicVertAngle (0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク0のメイン応答軸 (MRA) 垂直角度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>46</p></td>
<td align="left"><p>wMicHorAngle (0)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク0の MRA 水平方向の角度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>マイクの定義1から n-1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>34 + ((n-1)<em>12)</p></td>
<td align="left"><p>wMicType (n-1)</p></td>
<td align="left"></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイクの種類を一意に識別する数値 (n-1):</p>
<p>00: 双方向</p>
<p>01: SubCardioid</p>
<p>02: cardioid</p>
<p>03: SuperCardioid</p>
<p>04: HyperCardioid</p>
<p>05: 8 整形</p>
<p>0F-FF: ベンダーが定義済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>36 + ((n-1)</em>12)</p></td>
<td align="left"><p>wXCoordinate (n-1)</p></td>
<td align="left"></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク n-1 の x 座標。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>38 + ((n-1)<em>12)</p></td>
<td align="left"><p>wYCoordinate (n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク n-1 の y 座標。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40 + ((n-1)</em>12)</p></td>
<td align="left"><p>wZCoordinate (n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク n-1 の z 座標。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>42 + ((n-1)<em>12)</p></td>
<td align="left"><p>wMicVertAngle (n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク n-1 の MRA 垂直角度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>44 + ((n-1)</em>12)</p></td>
<td align="left"><p>wMicHorAngle (n-1)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Number</p></td>
<td align="left"><p>マイク n-1 の MRA 水平方向の角度。</p></td>
</tr>
</tbody>
</table>

4要素のマイク配列の記述子でこの情報形式を使用する方法の詳細な例については、「 [Windows Vista 用のマイク配列を構築して使用する方法](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/MicArrays_guide.doc)」ホワイトペーパーの付録 a を参照してください。

**注**  

-   マイク配列情報にバージョン番号を含めると、元の仕様が実装された後に記述子を更新できます。 バージョン番号は BCD の値です。 たとえば、現在のバージョン (1.0) は0x0100 として表されます。

-   オフセットとサイズの値はバイト単位です。

-   すべての角度は、1/10000 ラジアンの単位で表されます。 たとえば、3.1416 ラジアンは31416として表されます。 値は-31416 ~ 31416 の範囲で指定できます。

-   X-y 座標はミリメートル単位で表現されます。 値は-32767 ~ 32767 の範囲で指定できます。

-   座標系の回転角度の詳細については、前述の「マイク配列のホワイトペーパー」の付録 B を参照してください。

-   頻度の値は、Hz で表されます。 頻度の値の範囲は、 **Wworkspace freqバンド**のフィールドのサイズによってのみ制限さ**れます。**
