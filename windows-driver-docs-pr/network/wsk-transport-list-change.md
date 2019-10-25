---
title: WSK_TRANSPORT_LIST_CHANGE
description: WSK_TRANSPORT_LIST_CHANGE
ms.assetid: 3b12d692-467c-4d31-bd2a-bb6e34d87fde
ms.date: 07/18/2017
keywords:
- WSK_TRANSPORT_LIST_CHANGE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: abb30fc471c3035dd93fc27a11f6405c44c948aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844417"
---
# <a name="wsk_transport_list_change"></a>WSK\_TRANSPORT\_LIST\_の変更


WSK アプリケーションは WSK\_TRANSPORT\_LIST を使用して、使用可能なネットワークトランスポートの一覧が変更された場合に通知を受信するようにクライアントコントロールの制御操作を変更\_します。

使用可能なネットワークトランスポートの一覧が変更されたときに通知を受け取るには、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_TRANSPORT_LIST_CHANGE</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p>使用可能なネットワークトランスポートの一覧が変更されるまで WSK サブシステムによってキューに置かれる IRP へのポインター。 新しいネットワークトランスポートが追加されるか、既存のネットワークトランスポートが削除された後に、WSK サブシステムが IRP を完了します。</p></td>
</tr>
</tbody>
</table>

このクライアントコントロール操作には、IRP が必要です。

Wsk アプリケーションが[**Wskderegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)を呼び出して wsk サブシステムからデタッチする場合、wsk サブシステムは保留中の irp をキャンセルします。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




