---
title: WIA\_IP\_CUR\_インテント
description: WIA\_IP\_CUR\_インテントのプロパティには、アプリケーションのイメージの使用を目的の現在の設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 9fa732bb-9281-441e-91b5-ce6eec67ea8f
keywords:
- WIA_IPS_CUR_INTENT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_CUR_INTENT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8aa665d3abfe02727ae70bea93f62c1f6b22405
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556730"
---
# <a name="wiaipscurintent"></a>WIA\_IP\_CUR\_インテント


WIA\_IP\_CUR\_インテントのプロパティには、アプリケーションのイメージの使用を目的の現在の設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ips_cur_intent_si"></span><span id="DDK_WIA_IPS_CUR_INTENT_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_フラグ

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

ドライバーでは、インテントの設定を使用して、アプリケーションのイメージの使用を目的に基づく項目のプロパティを事前設定します。 これらのプロパティがあります、たとえば、品質が最大と最小サイズ。

次の表には、イメージ型のフラグとその定義が含まれています。 これらのフラグを使用する設定のイメージの種類が対象としています: 色、グレースケール、します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型のイメージ フラグ</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_INTENT_IMAGE_TYPE_COLOR</p></td>
<td><p>アプリケーションは、色スキャン デバイスを準備する予定です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_IMAGE_TYPE_GRAYSCALE</p></td>
<td><p>アプリケーションは、グレースケール スキャン デバイスを準備する予定です。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_IMAGE_TYPE_TEXT</p></td>
<td><p>アプリケーションは、テキストをスキャンするためにデバイスを準備する予定です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_IMAGE_TYPE_MASK</p></td>
<td><p>このフラグは、すべてのイメージ タイプのフラグのマスクです。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_NONE</p></td>
<td><p>既定値です。 目的が指定されていません。</p></td>
</tr>
</tbody>
</table>

 

次の表には、イメージのサイズと品質のフラグとその定義が含まれています。 これらのフラグは、画像のスキャンの品質とサイズの設定に使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イメージ サイズ/品質フラグします。</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_INTENT_BEST_PREVIEW</p></td>
<td><p>アプリケーションは、プレビューをスキャンするためにデバイスを準備する予定です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_MAXIMIZE_QUALITY</p></td>
<td><p>アプリケーションは、高品質な画像をスキャンするためにデバイスを準備する予定です。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_MINIMIZE_SIZE</p></td>
<td><p>アプリケーションは、小規模のスキャンで生成される画像をスキャンするためにデバイスを準備する予定です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_SIZE_MASK</p></td>
<td><p>このフラグは、すべてのサイズと品質のフラグのマスクです。</p></td>
</tr>
</tbody>
</table>

 

ドライバーは、他の設定選択されていることを目的の適切な判断を 1 インチあたりのドット数でビットの深さを選択します。 アプリケーションでは、プロパティが変更されたかを判断する現在の設定を読み取る必要があります。

アプリケーション設定、WIA\_IP\_CUR\_インテントのプロパティを自動取得の特定の目的の WIA プロパティを設定します。 フラグをビットごとの OR 演算子と組み合わせることができますが、画像がグレースケールと色の両方にすることはできませんに注意してください。

WIA\_IP\_CUR\_目的は、すべてのイメージの取得を有効になっている項目の必要な; は記憶域のアイテムまたはアイテムの保存されたイメージを使用できません。

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

 

 





