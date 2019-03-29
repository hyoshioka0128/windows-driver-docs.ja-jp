---
title: KSPROPERTY\_AEC\_モード
description: KSPROPERTY\_AEC\_モード プロパティを使用して、操作の AEC ノードのモードを制御します。 これは省略可能な AEC ノードのプロパティ (KSNODETYPE\_音響\_エコー\_キャンセル)。
ms.assetid: 79f0d655-4764-454f-8867-6cf1b5cedc82
keywords:
- KSPROPERTY_AEC_MODE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc1f71e2284382bef8ff2475c7515798a84b32b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571362"
---
# <a name="kspropertyaecmode"></a>KSPROPERTY\_AEC\_モード


KSPROPERTY\_AEC\_モード プロパティを使用して、操作の AEC ノードのモードを制御します。 これは省略可能な AEC ノードのプロパティ ([**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md))。

## <span id="ddk_ksproperty_aec_mode_ks"></span><span id="DDK_KSPROPERTY_AEC_MODE_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型のヘッダー ファイル Ksmedia.h から次のモードの定数のいずれかに設定することができます。

-   AEC\_モード\_渡す\_を通じて

    パススルー モードでは、AEC のノードは、キャプチャでき、変更されず、単にノードを通過するデータを表示します。

-   AEC\_モード\_半分\_双方向

    AEC アルゴリズムは、スピーカー フォンを操作に似ていますが、半二重モードで実行しています。 このモードでは、ローカル ユーザーの音声認識は、リモート ユーザーのより高いボリューム レベルにされるたびに、スピーカーの音量がミュートします。

-   AEC\_モード\_完全\_双方向

    AEC アルゴリズムは、全二重モードで実行されています。

パススルー モードでは、既定値です。 AEC ノードを含んでいるフィルターが作成されるか、ノードがリセットされた、ときに、ノードがパススルー モードで動作する初期構成されます。

Windows XP では、AEC のアルゴリズムの最初のリリースを[AEC システム フィルター](https://msdn.microsoft.com/library/windows/hardware/ff536174)使用が半二重モードをサポートしていません。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AEC\_モード プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

 

 






