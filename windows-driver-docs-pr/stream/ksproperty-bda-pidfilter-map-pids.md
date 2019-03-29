---
title: KSPROPERTY\_BDA\_PIDFILTER\_マップ\_PID
description: クライアントを使用して、KSPROPERTY\_BDA\_PIDFILTER\_マップ\_PID PID を通知するために、ダウン ストリームのフィルター ノードに渡す必要があるトランスポート ストリームのパケットの MPEG2 Pid の一覧のノードをフィルター処理します。
ms.assetid: 33d2775c-308a-4af0-81ae-b174990926ad
keywords:
- KSPROPERTY_BDA_PIDFILTER_MAP_PIDS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIDFILTER_MAP_PIDS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a63f6dafe9d59b164126c4b267b35f388ff2c3f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581548"
---
# <a name="kspropertybdapidfiltermappids"></a>KSPROPERTY\_BDA\_PIDFILTER\_マップ\_PID


クライアントを使用して、KSPROPERTY\_BDA\_PIDFILTER\_マップ\_PID PID を通知するために、ダウン ストリームのフィルター ノードに渡す必要があるトランスポート ストリームのパケットの MPEG2 Pid の一覧のノードをフィルター処理します。 このプロパティには、ノードでデータを配信するときに使用する出力型 (たとえばテーブル セクションまたはトランスポート ストリーム) の出力 PID フィルター ノードも通知します。

## <span id="ddk_ksproperty_bda_pidfilter_map_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_MAP_PIDS_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>BDA_PID_MAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**NodeId** KSP のメンバー\_ノードが PID フィルター ノードの識別子を指定します。

BDA\_PID\_マップ構造には、入力ストリームからフィルター処理するデータのマップがについて説明します。

PID フィルター ノードでは、ノードがダウン ストリーム渡して現在いる Pid の一覧で、このプロパティで提供されるリストを結合します。 指定されたリスト内の PID が PID フィルター ノードの一覧で既に場合は、指定された一覧の出力の種類が優先されます。 このプロパティは、型、ノードを出力するデータの取得にも使用されます。 BDA\_PID\_マップ構造には、この出力データのマップがについて説明します。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BDA\_PID\_マップ**](https://msdn.microsoft.com/library/windows/hardware/ff556534)

[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






