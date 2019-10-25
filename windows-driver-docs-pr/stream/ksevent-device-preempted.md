---
title: KSEVENT\_デバイス\_割り込まれる
description: KSEVENT\_DEVICE\_プリエンプションイベントは、デバイスが割り込まれたときにトリガーされます。
ms.assetid: A51B7109-AFBE-4849-9655-F913FB7851F1
keywords:
- KSEVENT_DEVICE_PREEMPTED ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSEVENT_DEVICE_PREEMPTED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f2b100f789f1a27d366fd2239a65cc6de771be2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844923"
---
# <a name="ksevent_device_preempted"></a>KSEVENT\_デバイス\_割り込まれる


**KSEVENT\_device\_プリエンプション**イベントは、デバイスが割り込まれたときにトリガーされます。

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

次のシナリオでは、プリエンプションイベントがトリガーされます。

1.  最初は1つのカメラのみがシステムに接続され、Windows アプリはカメラからビデオをストリーミングします。
2.  2つ目の Windows アプリは、キャプチャスタックが最初のアプリからデバイスを横取りし、2番目のアプリに制御を与えることを要求します。
3.  この要求が発行されると、ドライバーは、 **KSEVENT\_デバイス\_割り込ま**れるイベントを両方の Windows アプリに送信します。

## <a name="see-also"></a>関連項目


[**KSEVENT\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksevent_device)

[**KSEVENT\_デバイス\_失われました**](ksevent-device-lost.md)

 

 






