---
title: WIA\_IP\_サポートされている\_バーコード\_型
description: WIA\_IP\_サポートされている\_バーコード\_型のプロパティ リストのすべてのバーコードの種類がサポートされているバーコード リーダーでは、(認識) に WIA ミニドライバーによって使用されます。
ms.assetid: 38CA1167-25DB-4495-B31A-F996671E2686
keywords:
- WIA_IPS_SUPPORTED_BARCODE_TYPES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_SUPPORTED_BARCODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c454e2deea3ad0f27476f75fff549f8541f59cd9
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464274"
---
# <a name="wiaipssupportedbarcodetypes"></a>WIA\_IP\_サポートされている\_バーコード\_型


**WIA\_IP\_サポートされている\_バーコード\_型**プロパティ リストのすべてのバーコードの種類がサポートされているバーコード リーダーでは、(認識) に WIA ミニドライバーによって使用されます。 サポートされているバーコードのタイプは、VT で報告される\_として複数のエントリを含む 1 つの値のベクターの配列。




プロパティの種類:VT\_I4 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE (1 つの配列/ベクトル値)

アクセス権:読み取り専用です。

<a name="remarks"></a>コメント
-------

次の表に、有効な値、 **WIA\_IP\_サポートされている\_バーコード\_型**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>[値]</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_BARCODE_UPCA</p></td>
<td><p>Universal Product Code UPC A</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_UPCE</p></td>
<td><p>Universal Product Code UPC-e</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODABAR</p></td>
<td><p>Codabar コード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_NONINTERLEAVED_2OF5</p></td>
<td><p>5 の 2 つアウト コード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_INTERLEAVED_2OF5</p></td>
<td><p>5 つのコードのインターリーブ 2</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE39</p></td>
<td><p>Code 39</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE39_MOD43</p></td>
<td><p>コード 39 mod 43</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE39_FULLASCII</p></td>
<td><p>完全な ASCII コード 39</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE93</p></td>
<td><p>コード 93</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE128</p></td>
<td><p>Code 128</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE128A</p></td>
<td><p>コード 128A</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE128B</p></td>
<td><p>コード 128B</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE128C</p></td>
<td><p>128 C コード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_GS1128</p></td>
<td><p>GS1 128 (旧称 UCC ean 協会/128)</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_GS1DATABAR WIA_BARCODE_ITF14</p></td>
<td><p>GS1 DataBar コード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_ITF14</p></td>
<td><p>ITF 14 コード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_EAN8</p></td>
<td><p>Ean 協会 8 コード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_EAN13</p></td>
<td><p>Ean 協会 13 コード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTNETA</p></td>
<td><p>POSTNET (郵便番号数値エンコード技法)"A"のコード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_POSTNETB</p></td>
<td><p>POSTNET (郵便番号数値エンコード技法)"B"のコード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTNETC</p></td>
<td><p>POSTNET (郵便番号数値エンコード技法)"C"コード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_POSTNET_DPBC</p></td>
<td><p>POSTNET (郵便番号数値エンコード技法) DPBC (バーコード) コード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_PLANET</p></td>
<td><p>郵便番号アルファ数値のエンコーディング方法 (惑星)</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_INTELLIGENT_MAIL</p></td>
<td><p>インテリジェントなメール バーコードが (POSTNET と地球のバーコードを置換)</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTBAR</p></td>
<td><p>PostBar (とも呼ばれます CPC 4-状態)</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_RM4SCC</p></td>
<td><p>RM4SCC バーコード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_HIGH_CAPACITY_COLOR</p></td>
<td><p>Microsoft 高容量のカラー バーコード (HCCB)</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_MAXICODE</p></td>
<td><p>MaxiCode</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_PDF417</p></td>
<td><p>PDF417 バーコード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CPCBINARY</p></td>
<td><p>CPC バイナリ バーコード (カナダの投稿)</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_FIM</p></td>
<td><p>顔識別マーク (FIM) バーコード (USPS)</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_PHARMACODE</p></td>
<td><p>医薬品のバイナリ コード (Pharmacode)</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_PLESSEY</p></td>
<td><p>Plessey コード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_MSI</p></td>
<td><p>MSI (変更 Plessey) コード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_JAN</p></td>
<td><p>コードの日本語の文書番号 (1 月)</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_TELEPEN</p></td>
<td><p>Telepen コード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_AZTEC</p></td>
<td><p>アステカ コード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_SMALLAZTEC</p></td>
<td><p>小さなアステカ コード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_DATAMATRIX</p></td>
<td><p>データのマトリックス コード</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_DATASTRIP</p></td>
<td><p>Datastrip コード (Cauzin Softstrip)</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_EZCODE</p></td>
<td><p>Ezcode</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_QRCODE</p></td>
<td><p>QR コード</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_SHOTCODE</p></td>
<td><p>ShotCode</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_SPARQCODE</p></td>
<td><p>SPARQCode</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CUSTOM_BASE + N</p></td>
<td><p>WIA_BARCODE_CUSTOM_BASE は、WIA ミニドライバーを追加するすべてのカスタムのバーコード値にオフセットです。 N は、正の整数です。</p></td>
</tr>
</tbody>
</table>

 

WIA ミニドライバーは、WIA として定義されている追加のカスタム値でこのリストを拡張することができます\_バーコード\_カスタム\_基本 + N、N は正の整数。

このプロパティは、バーコード リーダーのすべての項目に必要です。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





