---
title: プロトコル バインドの状態と操作
description: プロトコル バインドの状態と操作
ms.assetid: 669b3de1-7f6b-4e63-8943-c8eaadfa80fc
keywords:
- プロトコルドライバー WDK ネットワーク、バインド動作状態
- NDIS プロトコルドライバー WDK、バインド操作の状態
- バインドの状態 WDK ネットワーク
- プロトコルドライバー WDK ネットワーク、イベント
- NDIS プロトコルドライバー WDK、イベント
- イベント WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b74e4e019b2aec5f2ae196e2d2b5c76b56b71cfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843476"
---
# <a name="protocol-binding-states-and-operations"></a>プロトコル バインドの状態と操作





NDIS プロトコルドライバーでは、ドライバーが管理する各バインドについて、次の動作状態がサポートされている必要があります。

<a href="" id="unbound"></a>非バインド  
バインド解除された状態は、バインディングの初期状態です。 この状態では、プロトコルドライバーは NDIS が[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すまで待機します。

<a href="" id="opening"></a>左中  
オープン状態では、プロトコルドライバーはバインドのリソースを割り当て、アダプターを開こうとします。

<a href="" id="running"></a>起動  
実行中の状態では、プロトコルドライバーはバインドの送信および受信処理を実行します。

<a href="" id="closing"></a>右山  
終了状態では、プロトコルドライバーはアダプターへのバインディングを閉じ、バインディングのリソースを解放します。

<a href="" id="pausing"></a>一時停止  
一時停止中の状態では、バインドの送信および受信操作を停止するために必要なすべての操作が、プロトコルドライバーによって完了されます。

<a href="" id="paused"></a>中  
一時停止状態では、プロトコルドライバーはバインドに対して送信操作または受信操作を実行しません。

<a href="" id="restarting"></a>再起動  
再起動状態では、プロトコルドライバーは、バインディングの送信および受信操作を再開するために必要なすべての操作を完了します。

次の表では、ヘッダーはバインド状態を表し、イベントは最初の列に一覧表示されています。 テーブル内の残りのエントリは、状態内でイベントが発生した後にバインドが入力する次の状態を指定します。 空のエントリは、無効なイベントと状態の組み合わせを表します。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント \ 状態</th>
<th align="left">非バインド</th>
<th align="left">左中</th>
<th align="left">右山</th>
<th align="left">一時停止</th>
<th align="left">再起動</th>
<th align="left">実行中</th>
<th align="left">一時停止</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ProtocolBindAdapterEx</em></p></td>
<td align="left"><p>左中</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>バインドに失敗しました</p></td>
<td align="left"></td>
<td align="left"><p>非バインド</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>バインドが完了しました</p></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ProtocolUnbindAdapterEx</em></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>右山</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>バインド解除が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>非バインド</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>PnP 一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>一時停止が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="even">
<td align="left"><p>PnP の再起動</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>再起動</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>再起動が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>実行中</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>再起動に失敗しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>送信および受信操作</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="even">
<td align="left"><p>OID 要求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>右山</p></td>
<td align="left"><p>一時停止</p></td>
<td align="left"><p>再起動</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
</tbody>
</table>

 

前の表に記載されているイベントは、NDIS プロトコルバインドの主要なイベントで  **ことに注意**してください。 情報が使用可能になると、このテーブルに追加のイベントが追加されます。

 

プライマリバインディングイベントは、次のように定義されます。

<a href="" id="protocolbindadapterex"></a>*ProtocolBindAdapterEx*  
NDIS がドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出した後、バインディングは開始状態になります。 詳細については、「[アダプターへのバインド](binding-to-an-adapter.md)」を参照してください。

<a href="" id="bind-failed"></a>バインドに失敗しました  
プロトコルドライバーがアダプターへのバインドに失敗した場合、バインドはバインドされていない状態に戻ります。

<a href="" id="bind-is-complete"></a>バインドが完了しました  
ドライバーがアダプターを正常に開くと、バインドは一時停止状態になります。 ドライバーはバインド操作を完了します。

<a href="" id="protocolunbindadapterex"></a>*ProtocolUnbindAdapterEx*  
NDIS がドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)ハンドラーを呼び出した後、バインディングは*終了*状態になります。 詳細については、「[アダプターからのバインド](unbinding-from-an-adapter.md)解除」を参照してください。

<a href="" id="unbind-is-complete"></a>バインド解除が完了しました  
ドライバーがバインド解除操作を完了すると、バインドはバインドされていない状態になります。

<a href="" id="pnp-pause"></a>PnP 一時停止  
NDIS がプロトコルドライバーを送信した後、ネットワークプラグアンドプレイ (PnP) 一時停止イベント通知を送信すると、バインドは一時停止中の状態になります。 詳細について[は、「バインディングの一時停止](pausing-a-binding.md)」を参照してください。

<a href="" id="pause-is-complete"></a>一時停止が完了しました  
送信と受信の操作を停止するために必要なすべての操作がドライバーによって完了すると、一時停止操作が完了し、バインドが一時停止状態になります。

一時停止操作が完了する前に、すべての未処理の送信要求が完了するまでドライバーが待機する必要がある  に**注意**してください。

 

<a href="" id="pnp-restart"></a>PnP の再起動  
NDIS によって、ネットワークの PnP 再起動イベント通知がプロトコルドライバーに送信された後、バインドは再起動状態になります。 詳細については、「[バインディングの再起動](restarting-a-binding.md)」を参照してください。

<a href="" id="restart-is-complete"></a>再起動が完了しました  
ドライバーが送受信操作を処理できるようになると、再起動操作が完了し、バインドが実行中の状態になります。

<a href="" id="restart-failed"></a>再起動に失敗しました  
NDIS がプロトコルドライバーを送信してネットワークの PnP 再起動イベント通知を送信し、再起動の試行が失敗した場合、バインドは一時停止状態に戻ります。

<a href="" id="send-and-receive-operations"></a>送信および受信操作  
プロトコルドライバーは、実行中および一時停止中の状態の送信および受信操作を処理する必要があります。 送信操作と受信操作の詳細については、「[プロトコルドライバーの送信および受信操作](protocol-driver-send-and-receive-operations.md)」を参照してください。

<a href="" id="oid-requests"></a>OID 要求  
プロトコルドライバーは、基になるドライバーの情報を設定または照会するための OID 要求を開始できます。 プロトコルドライバーは、バインドされていない状態を除き、すべての状態から OID 要求を開始できます。

## <a name="related-topics"></a>関連トピック


[NDIS プロトコルドライバーの記述](writing-ndis-protocol-drivers.md)

 

 






