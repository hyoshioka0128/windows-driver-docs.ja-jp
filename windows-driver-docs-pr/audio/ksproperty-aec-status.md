---
title: KSPROPERTY\_AEC\_状態
description: KSPROPERTY\_AEC\_AEC ノードの状態を監視する STATUS プロパティが使用される (KSNODETYPE\_音響\_エコー\_キャンセル)。 これは、AEC のノードのオプションのプロパティです。
ms.assetid: cd344367-1cb3-425a-8b22-300a85514e20
keywords:
- KSPROPERTY_AEC_STATUS オーディオ デバイス
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
ms.openlocfilehash: 982d0b18fe330785cadc60810c8c205c1dfb9642
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528437"
---
# <a name="kspropertyaecstatus"></a>KSPROPERTY\_AEC\_状態


KSPROPERTY\_AEC\_AEC ノードの状態を監視する STATUS プロパティが使用される ([**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)). これは、AEC のノードのオプションのプロパティです。

## <span id="ddk_ksproperty_aec_status_ks"></span><span id="DDK_KSPROPERTY_AEC_STATUS_KS"></span>


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
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は、ULONG 型です。 これは、フラグのビットの左側にある次の表では、Ksmedia.h のヘッダー ファイルで定義されている 1 つ以上のビットごとの OR に設定できる状態の値です。 対応する DSCFX\_AEC\_Dsound.h のヘッダー ファイルからの状態フラグは、テーブルの右側の列に表示されます。 これらのフラグについては、Microsoft Windows SDK ドキュメントを参照してください。

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

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AEC\_プロパティの状態要求のステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

AEC の状態フラグの 3 つの最下位ビットは、AEC のアルゴリズムの収束履歴 (CH) を表します (前の表を参照してください)。 CH ステータス ビットは、アルゴリズムは集中しているかどうかとデータの処理が開始された時刻以降収束された状態で維持がかどうかを判断する Microsoft DirectSound アプリケーションで使用できます。 オーディオのハードウェアによって AEC アルゴリズムこの場合、結果として得られるキャプチャ バッファーは、スピーカーからエコーが含まれる可能性に収束すると、失敗可能性があります。

AEC ノードを含むフィルターを作成またはノードがリセットされる、AEC のアルゴリズムは 3 つの CH ステータス ビットを最初をゼロに設定します。 この設定は、初期化されていない状態、AEC を表す\_状態\_FD\_履歴\_初期化されていません。

収束の状態では、AEC に切り替わります。 CH 状態 AEC アルゴリズムが収束後\_状態\_FD\_履歴\_継続的に\_収束します。 CH 状態が、AEC が困難になった状態に切り替わります AEC アルゴリズムがこれまでの収束を失った場合\_状態\_FD\_履歴\_以前\_DIVERGED します。 状態は収束された状態からが困難になった状態に切り替えるには最も高いですが、その可能性がありますに切り替えることも、初期化されていない状態から直接が困難になった状態。 CH 状態が困難になった状態に切り替えてから、アルゴリズムがリセットまたはスタベーションになるまでの状態の検出に保持されます。

ときに、 [AEC システム フィルター](https://msdn.microsoft.com/library/windows/hardware/ff536174) --その 4 つのピンのいずれかの不足を検出した収束履歴を含む、その内部状態にリセットでキャプチャ、キャプチャした、では、レンダリングまたは--をレンダリングします。

次の 3 つの CH ステータス ビットのビット 2 が現在使用されていないに注意してください。

CH ステータス ビットを使用する代わりに、アプリケーションは、AEC をチェックしてリアルタイムの収束の状態を監視できます\_状態\_FD\_現在\_収束フラグ ビットです。 このビットが設定されている場合、アルゴリズムが現在集約します。 アルゴリズム音響パスが変更された場合に一時的に収束が失われることができます。 このような一時的な損失が不適切な CH ステータス ビットを DSCFX に切り替えることを防ぐために、リアルタイムの収束フラグがフィルター選択された\_AEC\_状態\_FD\_履歴\_以前\_困難になった状態です。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

 

 






