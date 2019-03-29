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
ms.openlocfilehash: 0ff08883cb30e3de24032a11728d9c7329b8a65d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580659"
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
<th>Set</th>
<th>移行先</th>
<th>イベント記述子の種類</th>
<th>イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561744" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561744)"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

プリエンプション イベントは、次のシナリオでトリガーされます。

1.  初期状態のみ 1 つのカメラは、システムにアタッチされ、Windows アプリがカメラからビデオをストリーミングします。
2.  2 つ目の Windows アプリでは、キャプチャのスタックが最初のアプリからデバイスを切断し、2 つ目のアプリに制御を要求します。
3.  この要求が発行されたときに、ドライバーの送信、 **KSEVENT\_デバイス\_割り込み**イベント両方の Windows アプリをします。

## <a name="see-also"></a>関連項目


[**KSEVENT\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/jj151588)

[**KSEVENT\_デバイス\_LOST**](ksevent-device-lost.md)

 

 






