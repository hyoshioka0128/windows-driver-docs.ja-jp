---
title: KSPROPERTY\_FMRX\_状態
description: KSPROPERTY\_FMRX\_状態プロパティは、FM ラジオが有効になっているかどうかを指定します。
ms.assetid: A975221C-3300-4A44-9E8C-9AB4B4C54C32
keywords:
- KSPROPERTY_FMRX_STATE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_FMRX_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75f08c976f41dcd042511b7a4b68f023348e13d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571550"
---
# <a name="kspropertyfmrxstate"></a>KSPROPERTY\_FMRX\_状態


**KSPROPERTY\_FMRX\_状態**プロパティは、FM ラジオが有効になっているかどうかを指定します。

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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は BOOL 型で、FM ラジオが有効になっているかどうかを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_FMRX\_状態**プロパティ要求を返します**TRUE** FM ラジオが有効になっている場合と**FALSE** FM ラジオが無効になっている場合。

<a name="remarks"></a>コメント
-------

FM ラジオを有効または、設定を無効になっている、 **KSPROPERTY\_FMRX\_状態**wave フィルターのプロパティ。 FM ボリュームとルーティング (エンドポイントの選択) によって制御されます、 [ **KSPROPERTY\_FMRX\_ボリューム**](ksproperty-fmrx-volume.md)と[ **KSPROPERTY\_FMRX\_ENDPOINTID** ](ksproperty-fmrx-endpointid.md)トポロジ フィルターのプロパティ。 基本的なサポート、 **KSPROPERTY\_FMRX\_ボリューム**プロパティは、最小のボリューム、最大のボリュームとボリュームの範囲を返す必要があります。

新しい[ **KSNODETYPE\_FM\_RX** ](ksnodetype-fm-rx.md)システムでは、他のオーディオ エンドポイントがあり、すべてのオーディオのエンドポイント プロパティがサポートしているトポロジ ノードのエンドポイントが実装されます。 このエンドポイントで定義されている回線のモジュラー ジャック プロパティもサポートしています。、 [KSPROPSETID\_ジャック](kspropsetid-jack.md)プロパティ セット。 このエンドポイントは起動時に接続されていない状態です。 FM ラジオをキャプチャすると、ドライバーでサポートされて、このエンドポイントがアクティブになります FM ラジオが有効にするとします。 ピン留め、キャプチャの作成、 **KSNODETYPE\_FM\_RX**トポロジのノードでは、FM 受信者から経由で送信されるオーディオ キャプチャします。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クライアント</p></td>
<td align="left"><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





