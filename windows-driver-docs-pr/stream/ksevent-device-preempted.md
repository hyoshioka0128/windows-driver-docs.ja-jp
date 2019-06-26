---
title: KSEVENT\_デバイス\_割り込み
description: KSEVENT\_デバイス\_デバイスが切断されていると、割り込みイベントがトリガーされます。
ms.assetid: A51B7109-AFBE-4849-9655-F913FB7851F1
keywords:
- KSEVENT_DEVICE_PREEMPTED ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSEVENT_DEVICE_PREEMPTED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ab1390ddb04d81fe6aa2e685ba4f125a4fe799
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391714"
---
# <a name="kseventdevicepreempted"></a>KSEVENT\_デバイス\_割り込み


**KSEVENT\_デバイス\_割り込み**デバイスが割り込まれましたときにイベントがトリガーされます。

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
<td><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プリエンプション イベントは、次のシナリオでトリガーされます。

1.  初期状態のみ 1 つのカメラは、システムにアタッチされ、Windows アプリがカメラからビデオをストリーミングします。
2.  2 つ目の Windows アプリでは、キャプチャのスタックが最初のアプリからデバイスを切断し、2 つ目のアプリに制御を要求します。
3.  この要求が発行されたときに、ドライバーの送信、 **KSEVENT\_デバイス\_割り込み**イベント両方の Windows アプリをします。

## <a name="see-also"></a>関連項目


[**KSEVENT\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksevent_device)

[**KSEVENT\_デバイス\_LOST**](ksevent-device-lost.md)

 

 






