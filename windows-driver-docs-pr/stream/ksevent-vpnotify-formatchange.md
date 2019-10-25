---
title: KSEVENT\_VPNOTIFY\_FORMATCHANGE
description: KSEVENT\_VPNOTIFY\_FORMATCHANGE イベントは、ビデオ形式の変更などのイベントを、カーネルモードの DVD デコーダーミニドライバーからユーザーモードの DirectShow に伝達するために使用されます。
ms.assetid: 4c1757ec-1453-4aaa-b246-7c255e29310d
keywords:
- KSEVENT_VPNOTIFY_FORMATCHANGE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSEVENT_VPNOTIFY_FORMATCHANGE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4956e92688c220e26dceb90f92d1395cf14064a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843667"
---
# <a name="ksevent_vpnotify_formatchange"></a>KSEVENT\_VPNOTIFY\_FORMATCHANGE


KSEVENT\_VPNOTIFY\_FORMATCHANGE イベントは、ビデオ形式の変更などのイベントを、カーネルモードの DVD デコーダーミニドライバーからユーザーモードの DirectShow に伝達するために使用されます。

## <span id="ddk_ksevent_vpnotify_formatchange_ks"></span><span id="DDK_KSEVENT_VPNOTIFY_FORMATCHANGE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

ミニドライバーは、解像度が 640 x 480 から 720 x 480 に変更されたなど、ビデオ形式の変更を検出できます。 この形式の変更についてユーザーモードコンポーネントに通知する必要があります。これにより、必要なアクションが DirectShow フィルターと Ksk プロキシの間で実行されるようになります。

Ksk プロキシの VPE フィルターは、このイベントを使用して、Win32 API CreateEvent を使用して作成されたユーザーモードのイベントハンドルをミニドライバーに渡します。このイベントハンドルは、イベントハンドルを保存する必要があります。

ミニドライバーは、後でこのイベントハンドルを設定して、KsProxy VPE フィルターに通知します。これにより、新しいビデオ形式に基づいて接続が再度ネゴシエートされます。

KsProxy VPE フィルターは、IOCTL\_KS\_送信することによってイベント通知を無効にし、同じイベントハンドルを使用して\_イベント i/o 制御コードを無効にします。 次に、イベントハンドルが VPE フィルターによって閉じられます。 ミニドライバーは、イベントハンドルを閉じることはできません。

DirectShow フィルターと Ksk プロキシの詳細については、「[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。 ビデオ解像度の変更など、ストリームの変更を処理する方法の詳細については、「[変更のストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/stream-changes)」を参照してください。

 

 





