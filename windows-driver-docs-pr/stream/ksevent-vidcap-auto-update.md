---
title: KSEVENT\_VIDCAP\_自動\_更新
description: プロパティ値が変更されると、KSEVENT\_VIDCAP\_AUTO\_UPDATE イベントがトリガーされます。
ms.assetid: dd7e665f-104d-4276-94aa-62d64faba69d
keywords:
- KSEVENT_VIDCAP_AUTO_UPDATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSEVENT_VIDCAP_AUTO_UPDATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ee65eb06fa34f7995517ed3cfb0605157a6d19
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843676"
---
# <a name="ksevent_vidcap_auto_update"></a>KSEVENT\_VIDCAP\_自動\_更新


プロパティ値が変更されると、KSEVENT\_VIDCAP\_AUTO\_UPDATE イベントがトリガーされます。

## <span id="ddk_ksevent_vidcap_auto_update_ks"></span><span id="DDK_KSEVENT_VIDCAP_AUTO_UPDATE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>イベント記述子の種類</th>
<th>イベント値の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クライアントは、ユーザーがデバイスのスイッチを反転してプロパティ値を変更した場合に通知されるように、このイベントに登録することができます。 このイベントを使用できるようにするには、ハードウェアの実装でこの機能のサポートを提供する必要があります。

DirectShow フィルターと Ksk プロキシの詳細については、「[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。

 

 





