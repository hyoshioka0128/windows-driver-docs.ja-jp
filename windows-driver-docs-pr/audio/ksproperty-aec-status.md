---
title: KSK プロパティ\_AEC\_状態
description: "\"KSK\" プロパティ\\_AEC\\_STATUS プロパティは、AEC ノードの状態を監視するために使用されます (KSNODETYPE\\_音響\\_ECHO\\_CANCEL)。 これは、AEC ノードの省略可能なプロパティです。"
ms.assetid: cd344367-1cb3-425a-8b22-300a85514e20
keywords:
- KSPROPERTY_AEC_STATUS オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e295238892636fd1d4db7ef6e7ae6bd3d0b99b0a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833069"
---
# <a name="ksproperty_aec_status"></a>KSK プロパティ\_AEC\_状態


"KSK" プロパティ\_AEC\_STATUS プロパティは、AEC ノードの状態を監視するために使用されます ([**KSNODETYPE\_音響\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md))。 これは、AEC ノードの省略可能なプロパティです。

## <span id="ddk_ksproperty_aec_status_ks"></span><span id="DDK_KSPROPERTY_AEC_STATUS_KS"></span>


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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は ULONG です。 これは、次の表の左側の列にある1つ以上のフラグビットのビットごとの OR に設定できる状態値です。この値は、ヘッダーファイル Ksmedia .h に定義されています。 対応する DSCFX\_AEC\_ヘッダーファイル Dsound からの状態フラグが、テーブルの右側の列に表示されます。 これらのフラグの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">AEC の状態フラグ</th>
<th align="left">Value</th>
<th align="left">DSCFX_AEC_STATUS フラグ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AEC_STATUS_FD_HISTORY_UNINITIALIZED</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>DSCFX_AEC_STATUS_HISTORY_UNINITIALIZED</p></td>
</tr>
<tr class="even">
<td align="left"><p>AEC_STATUS_FD_HISTORY_CONTINUOUSLY_CONVERGED</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>DSCFX_AEC_STATUS_HISTORY_CONTINUOUSLY_CONVERGED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AEC_STATUS_FD_HISTORY_PREVIOUSLY_DIVERGED</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>DSCFX_AEC_STATUS_HISTORY_PREVIOUSLY_DIVERGED</p></td>
</tr>
<tr class="even">
<td align="left"><p>AEC_STATUS_FD_CURRENTLY_CONVERGED</p></td>
<td align="left"><p>0x8</p></td>
<td align="left"><p>DSCFX_AEC_STATUS_CURRENTLY_CONVERGED</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AEC\_STATUS プロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

AEC 状態フラグの最下位3ビット (上記の表を参照) は、AEC アルゴリズムの収束履歴 (CH) を表します。 Microsoft DirectSound アプリケーションでは、CH status ビットを使用して、アルゴリズムが収束したかどうか、およびデータの処理を開始してから収束状態になったかどうかを判断できます。 オーディオハードウェアによっては、AEC アルゴリズムが収束しないことがあります。この場合、結果として得られるキャプチャバッファーには、スピーカーからのエコーが含まれる可能性があります。

AEC ノードを含むフィルターが作成されるか、ノードがリセットされると、AEC アルゴリズムは最初に3つの CH status ビットを0に設定します。 この設定は、初期化されていない状態、AEC\_ステータス\_FD\_履歴\_初期化されていない状態を表します。

AEC アルゴリズムが収束すると、CH status は収束状態に切り替わり、AEC\_STATUS\_FD\_履歴\_継続的に収束\_ます。 AEC アルゴリズムによって収束が失われた場合、CH status は分岐状態、AEC\_STATUS\_FD\_\_履歴に切り替わり、以前は分岐\_ます。 状態は、収束状態から分岐状態に切り替える可能性が最も高くなりますが、初期化されていない状態から分岐状態に直接切り替えることもできます。 CH status は分岐状態に切り替えられた後、アルゴリズムがリセットされるか、または枯渇が検出されるまで、その状態のままになります。

[AEC システムフィルター](https://docs.microsoft.com/windows-hardware/drivers/audio/aec-system-filter)が4つの任意のピンでの枯渇を検出した場合 (キャプチャイン、キャプチャ、レンダリング、またはレンダリング)、その内部状態 (収束履歴を含む) がリセットされます。

この3つの CH status ビットのビット2は現在使用されていないことに注意してください。

CH status ビットを使用する代わりに、アプリケーションでは、AEC\_STATUS\_FD\_現在\_収束フラグビットであることを確認して、リアルタイムの収束状態を監視できます。 このビットが設定されている場合、アルゴリズムは現在収束されています。 音響パスで変更が発生すると、アルゴリズムが一時的に収束しなくなる可能性があります。 リアルタイムの収束フラグをフィルター処理して、CH status ビットを DSCFX\_AEC\_STATUS\_FD\_HISTORY\_以前\_分岐 state に不適切に切り替えることができないようにします。

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

 

 






