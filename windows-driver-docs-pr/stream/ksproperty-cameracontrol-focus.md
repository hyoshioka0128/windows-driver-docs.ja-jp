---
title: KSPROPERTY\_CAMERACONTROL\_フォーカス
description: ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_フォーカス プロパティを取得またはカメラのフォーカスの設定を設定します。 このプロパティは省略可能です。
ms.assetid: 89a77055-1ad1-4394-8435-d057685b9eee
keywords:
- KSPROPERTY_CAMERACONTROL_FOCUS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a65920f9afd7511178d3247f2f595280bac213d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341823"
---
# <a name="kspropertycameracontrolfocus"></a>KSPROPERTY\_CAMERACONTROL\_フォーカス


ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_フォーカス プロパティを取得またはカメラのフォーカスの設定を設定します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_cameracontrol_focus_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_FOCUS_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、フォーカスの設定を指定する LONG が。 この値は、ミリメートル単位で表されます。

**注意**  記述またはアプリをテストする場合を実際には、ドライバーによって、カスタムの範囲を定義フォーカスと標準的な単位に基づかないがカスタム ステップ値に注意してくださかった。 ドライバーは、物理的にまたはデジタル フォーカス コントロールを実装できます。

 

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_の構造は、フォーカス設定を指定します。

このプロパティをサポートするすべてのビデオ キャプチャ ミニドライバーは、このプロパティの独自の範囲と既定値を定義する必要があります。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564439)

 

 






