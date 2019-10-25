---
title: MB ミニポート ドライバー エラー ログ
description: MB ミニポート ドライバー エラー ログ
ms.assetid: 57f83d03-29e5-4a20-8c0c-2d00954e7ccb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed3cfa5a7d5663a359f7aa8d411614789aaff63c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844287"
---
# <a name="mb-miniport-driver-error-logging"></a>MB ミニポート ドライバー エラー ログ


MB ミニポートドライバーは、次のように、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数で次のチェックを実行する必要があります。

-   MB ドライバーモデルをサポートするために必要な正しいデバイスファームウェアバージョンが存在すること。

-   デバイスと通信するために使用できる COM ポート。

-   リソースの競合はありません。

ミニポートドライバーが必要なリソースを取得できない場合は、MiniportInitializeEx 関数から NDIS\_STATUS\_リソースを返す必要があります。 ミニポートドライバーは、エラーの詳細を Windows イベントログに記録するために[**NdisWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteerrorlogentry)を呼び出す必要があります。

ミニポートドライバーでは、次の表の情報に従って、NdisWriteErrorLogEntry (ULONGs の可変サイズの配列) の呼び出しで、最後のパラメーターの最初の要素にエラーコードを指定する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_ERROR_UNSUPPORTED_FIRMWARE</p></td>
<td align="left"><p>デバイスは、サポートされていないファームウェアバージョンを実行しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_ERROR_COM_PORT_CONFLICT</p></td>
<td align="left"><p>デバイスと通信するための COM ポートを開くことができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_ERROR_RESOURCE_CONFLICT_OTHER</p></td>
<td align="left"><p>その他のリソースの競合。</p></td>
</tr>
</tbody>
</table>

 

ミニポートドライバーは、可変サイズの配列の残りの要素に他の値を設定できます。

 

 





