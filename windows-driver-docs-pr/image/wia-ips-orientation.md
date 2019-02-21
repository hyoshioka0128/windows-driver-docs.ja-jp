---
title: WIA\_IP\_向き
description: WIA\_IP\_ORIENTATION プロパティには、スキャンするドキュメントの現在の向きがについて説明します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: e963d0d1-020c-4ec1-8b67-a89b1fd3e545
keywords:
- WIA_IPS_ORIENTATION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_ORIENTATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fe506dc00a0b8c0ef8d50021fa11d2e78ca1959
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553534"
---
# <a name="wiaipsorientation"></a>WIA\_IP\_向き


WIA\_IP\_ORIENTATION プロパティには、スキャンするドキュメントの現在の向きがについて説明します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ips_orientation_si"></span><span id="DDK_WIA_IPS_ORIENTATION_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA\_IP\_ORIENTATION プロパティ ページまたは取得するイメージの元の方向を定義します。 WIA を使用する方法の詳細についての\_IP\_向きを参照してください[ **WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)します。

次の表に、WIA で有効な定数\_IP\_方向。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LANSCAPE</p></td>
<td><p>印刷の向きは、縦向きから 90 度反時計回りに回転します。</p></td>
</tr>
<tr class="even">
<td><p>縦向き</p></td>
<td><p>0 度の方向とは。</p></td>
</tr>
<tr class="odd">
<td><p>ROT180</p></td>
<td><p>印刷の向きは、縦向きから 180 度反時計回りに回転します。</p></td>
</tr>
<tr class="even">
<td><p>ROT270</p></td>
<td><p>方向は、縦向きを基準とした 270 度反時計回りに回転します。</p></td>
</tr>
</tbody>
</table>

 

WIA\_IP\_ORIENTATION プロパティには、スキャンするドキュメントの印刷の向きがについて説明します。 このプロパティは、スキャンの現在のフレームとページ サイズに影響します。

WIA\_IP\_ORIENTATIONis 異なります、 [ **WIA\_IP\_回転**](wia-ips-rotation.md)プロパティで、参照イメージに適用される回転する*後*をスキャンします。 したがってには、wia ROT180 値\_IP\_向きが wia ROT180 値と異なる\_IP\_回転します。 Wia\_IP\_向き、ROT180 のスキャン方向を基準とした、wia およびをスキャンする物理的なドキュメントの印刷の向きについて説明します\_IP\_回転、ROT180 がイメージに適用する回転をについて説明しますスキャンした後。

WIA\_IP\_方向プロパティは、ADF の項目に必要なその他のすべてのイメージの取得項目では省略可能。

**注**   WIA サービス内で互換レイヤーは WIA のサポートを追加していない\_IP\_向きプロパティがサポートされていない場合は、Microsoft Windows XP WIA デバイスから変換されたです、ADF の項目をデバイスの子項目。 ADF 項目がこのプロパティは常にサポートし、場合常に確認する必要があります、アプリケーションは期待できません WIA\_IP\_向きが実行時にサポートされています。

 

<a name="requirements"></a>要件
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

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)

[**WIA\_IP\_回転**](wia-ips-rotation.md)

 

 






