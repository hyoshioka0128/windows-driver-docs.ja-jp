---
title: KSEVENT\_VPNOTIFY\_段落
description: KSEVENT\_VPNOTIFY\_段落イベントは、ユーザー モードで DirectShow をカーネル モード DVD デコーダー ミニドライバーから、ビデオ形式の変更など、イベントが反映されるまでに使用されます。
ms.assetid: 4c1757ec-1453-4aaa-b246-7c255e29310d
keywords:
- KSEVENT_VPNOTIFY_FORMATCHANGE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSEVENT_VPNOTIFY_FORMATCHANGE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d05697309b7d8bfc3778d532482f8334fc9c1c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571139"
---
# <a name="kseventvpnotifyformatchange"></a>KSEVENT\_VPNOTIFY\_段落


KSEVENT\_VPNOTIFY\_段落イベントは、ユーザー モードで DirectShow をカーネル モード DVD デコーダー ミニドライバーから、ビデオ形式の変更など、イベントが反映されるまでに使用されます。

## <span id="ddk_ksevent_vpnotify_formatchange_ks"></span><span id="DDK_KSEVENT_VPNOTIFY_FORMATCHANGE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561937" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561937)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

ミニドライバー、ビデオ形式、解像度を 640 x 480 から 480 x 720 に変更する例については、変更を検出できます。 ユーザー モード コンポーネントは、必要なアクションは、DirectShow フィルターと KsProxy と配置を実行できるように、この形式の変更の通知する必要があります。

KsProxy の VPE フィルターは、イベントのハンドルを保存する必要がありますようにミニドライバーに、このイベントを使用して (Win32 API の CreateEvent を使用して作成された) ユーザー モード イベント ハンドルを渡します。

ミニドライバーは、後で、新しいビデオ形式に基づき、接続を再度ネゴシエートする KsProxy VPE フィルターに通知するには、このイベント ハンドルを設定します。

KsProxy VPE フィルターは、IOCTL を送信することによって、イベント通知を無効にします\_KS\_を無効にする\_同じイベント ハンドルを持つイベント I/O 制御コード。 VPE フィルターによってイベント ハンドルが閉じられます。 ミニドライバーは、イベント ハンドルを終了しないで必要があります。

DirectShow フィルターと KsProxy の詳細については、次を参照してください。[カーネル ストリーミング プロキシ](https://msdn.microsoft.com/library/windows/hardware/ff560877)します。 ビデオの解像度の変更などのストリームの変更の処理の詳細については、次を参照してください。 [Stream 変更](https://msdn.microsoft.com/library/windows/hardware/ff568284)します。

 

 





