---
title: KSK プロパティ\_AEC\_モード
description: KSK プロパティ\_AEC\_MODE プロパティは、AEC ノードの操作モードを制御するために使用されます。 これは、AEC ノードのオプションのプロパティです (KSNODETYPE\_音響\_ECHO\_CANCEL)。
ms.assetid: 79f0d655-4764-454f-8867-6cf1b5cedc82
keywords:
- KSPROPERTY_AEC_MODE オーディオデバイス
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
ms.openlocfilehash: 7d7cb680fc14c3dde6f4f9692b240f659cb72a10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831137"
---
# <a name="ksproperty_aec_mode"></a>KSK プロパティ\_AEC\_モード


KSK プロパティ\_AEC\_MODE プロパティは、AEC ノードの操作モードを制御するために使用されます。 これは、AEC ノードのオプションのプロパティです ([**KSNODETYPE\_音響\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md))。

## <span id="ddk_ksproperty_aec_mode_ks"></span><span id="DDK_KSPROPERTY_AEC_MODE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は ULONG で、ヘッダーファイル Ksmedia. h の次のいずれかのモード定数に設定できます。

-   AEC\_モード\_渡す\_

    パススルーモードでは、AEC ノードは、データのキャプチャとレンダリングを許可して、変更せずにノードをパススルーします。

-   AEC\_モード\_半\_双方向

    AEC アルゴリズムは、スピーカー電話に似た半二重モードで実行されています。 このモードでは、スピーカーの音量は、ローカルユーザーの音声がリモートユーザーの音量レベルより高い場合にミュートされます。

-   AEC\_モード\_全二重\_

    AEC アルゴリズムは、全二重モードで実行されています。

既定では、パススルーモードが使用されます。 AEC ノードを含むフィルターが作成されるか、ノードがリセットされると、ノードは最初にパススルーモードで動作するように構成されます。

Windows XP の最初のリリースでは、 [aec システムフィルター](https://docs.microsoft.com/windows-hardware/drivers/audio/aec-system-filter)が使用する aec アルゴリズムでは、ハーフデュプレックスモードはサポートされていません。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AEC\_MODE プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_音響\_ECHO\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

 

 






