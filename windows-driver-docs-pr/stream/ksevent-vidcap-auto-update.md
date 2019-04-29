---
title: KSEVENT\_しました\_自動\_UPDATE
description: KSEVENT\_しました\_自動\_プロパティ値が変更されたときに、更新イベントがトリガーされます。
ms.assetid: dd7e665f-104d-4276-94aa-62d64faba69d
keywords:
- KSEVENT_VIDCAP_AUTO_UPDATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSEVENT_VIDCAP_AUTO_UPDATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c748d84df8716cb1c37d29fc63953df482f57029
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324806"
---
# <a name="kseventvidcapautoupdate"></a>KSEVENT\_しました\_自動\_UPDATE


KSEVENT\_しました\_自動\_プロパティ値が変更されたときに、更新イベントがトリガーされます。

## <span id="ddk_ksevent_vidcap_auto_update_ks"></span><span id="DDK_KSEVENT_VIDCAP_AUTO_UPDATE_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th>イベント記述子の種類</th>
<th>イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561744" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561744)"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クライアントは、ユーザーからプロパティ値を変更するデバイスで、スイッチが反転する場合に通知するのには、このイベントの登録があります。 使用するには、このイベントのハードウェアの実装は、この機能のサポートを提供する必要があります。

DirectShow フィルターと KsProxy の詳細については、次を参照してください。[カーネル ストリーミング プロキシ](https://msdn.microsoft.com/library/windows/hardware/ff560877)します。

 

 





