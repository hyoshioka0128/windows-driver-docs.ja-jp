---
title: プロトコル バインドの状態と操作
description: プロトコル バインドの状態と操作
ms.assetid: 669b3de1-7f6b-4e63-8943-c8eaadfa80fc
keywords:
- プロトコル ドライバー WDK ネットワークは、バインドの操作状態
- NDIS プロトコル ドライバー WDK には、バインディング操作を状態します。
- バインドは、WDK ネットワークを状態します。
- プロトコル ドライバー WDK ネットワー キング、イベント
- NDIS プロトコル ドライバー WDK、イベント
- イベントの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d4945295c04ddfa9caac6ce95990b92c3fc81e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530543"
---
# <a name="protocol-binding-states-and-operations"></a>プロトコル バインドの状態と操作





NDIS プロトコル ドライバーはドライバーを管理する各バインドに次の操作の状態をサポートする必要があります。

<a href="" id="unbound"></a>バインドされていません。  
連結なしの状態は、バインディングの初期状態です。 この状態は、NDIS を呼び出すが待機プロトコル ドライバー、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。

<a href="" id="opening"></a>開始  
Opening 状態では、プロトコル ドライバーは、バインディングにリソースを割り当て、アダプターを開こうとするとします。

<a href="" id="running"></a>実行しています。  
実行中の状態では、プロトコル ドライバーは、送信を実行し、バインドの処理を受信します。

<a href="" id="closing"></a>閉じる  
Closing 状態にプロトコル ドライバー アダプターへのバインドを閉じて、バインディングのリソースを解放します。

<a href="" id="pausing"></a>一時停止  
一時停止中の状態では、プロトコル ドライバーは、送信を停止し、受信バインドの操作に必要なすべての操作を完了します。

<a href="" id="paused"></a>一時停止  
一時停止状態でプロトコル ドライバーにすれば、送信を実行または受信バインディングの操作はできません。

<a href="" id="restarting"></a>再起動します。  
再起動の状態では、プロトコル ドライバーは、送信を再起動し、受信バインドの操作に必要なすべての操作を完了します。

次の表に、見出しがバインドの状態を表すし、イベントは、最初の列に表示されます。 テーブル内のエントリの残りの部分は、[次へ] を指定のバインドは特定の状態でイベントが発生した後の入力を状態します。 空のエントリは、無効なイベントの状態の組み合わせを表します。

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
<th align="left">バインドされていません。</th>
<th align="left">開始</th>
<th align="left">閉じる</th>
<th align="left">一時停止</th>
<th align="left">再起動します。</th>
<th align="left">実行中</th>
<th align="left">一時停止</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ProtocolBindAdapterEx</em></p></td>
<td align="left"><p>開始</p></td>
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
<td align="left"><p>バインドされていません。</p></td>
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
<td align="left"><p>閉じる</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>バインド解除が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>バインドされていません。</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>PnP の一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>一時停止が完了</p></td>
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
<td align="left"><p>再起動します。</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>再起動が完了</p></td>
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
<td align="left"><p>送信し、受信操作</p></td>
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
<td align="left"><p>閉じる</p></td>
<td align="left"><p>一時停止</p></td>
<td align="left"><p>再起動します。</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
</tbody>
</table>

 

**注**  上記の表に示したイベントは、NDIS プロトコル バインドのプライマリのイベント。 追加のイベントは、情報が利用可能になった、このテーブルに追加されます。

 

プライマリ バインド イベントの定義は次のとおりです。

<a href="" id="protocolbindadapterex"></a>*ProtocolBindAdapterEx*  
NDIS ドライバーを呼び出してから[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数の場合、バインディングが Opening 状態に遷移します。 詳細については、次を参照してください。[をアダプターにバインド](binding-to-an-adapter.md)します。

<a href="" id="bind-failed"></a>バインドに失敗しました  
プロトコル ドライバーはアダプターにバインドできない場合、バインディングは連結なし状態に戻ります。

<a href="" id="bind-is-complete"></a>バインドが完了しました  
ドライバーでは、アダプターが正常に開き、バインドは一時停止状態になります。 ドライバーは、バインド操作を完了します。

<a href="" id="protocolunbindadapterex"></a>*ProtocolUnbindAdapterEx*  
NDIS ドライバーを呼び出してから[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)ハンドラー、バインドの入力、*閉じる*状態。 詳細については、次を参照してください。[アダプターからバインド解除](unbinding-from-an-adapter.md)します。

<a href="" id="unbind-is-complete"></a>バインド解除が完了しました  
ドライバーには、バインドの解除操作が完了すると、バインディングは連結なし状態になります。

<a href="" id="pnp-pause"></a>PnP の一時停止  
NDIS プロトコル ドライバーに送信した後、ネットワーク プラグ アンド プレイ (PnP) イベント通知を一時停止、バインドは一時停止状態になります。 詳細については、次を参照してください。[バインディングを一時停止](pausing-a-binding.md)します。

<a href="" id="pause-is-complete"></a>一時停止が完了  
ドライバーのために必要なすべての操作が完了した後操作の送受信を停止、一時停止操作が完了およびバインドが一時停止状態。

**注**  未処理の一時停止操作が完了する前に完了する要求を送信するすべてのドライバーが待つ必要があります。

 

<a href="" id="pnp-restart"></a>PnP の再起動  
NDIS は、プロトコル ドライバーにネットワーク PnP 再起動イベント通知を送信する後、バインドは再開中状態になります。 詳細については、次を参照してください。[バインディングを再起動する](restarting-a-binding.md)します。

<a href="" id="restart-is-complete"></a>再起動が完了  
準備ができたら、ドライバーを送信を処理し、受信操作では、再起動操作が完了と、バインディングが実行中の状態。

<a href="" id="restart-failed"></a>再起動に失敗しました  
NDIS ネットワーク PnP 再起動イベント通知が送信プロトコル ドライバー、再起動の試行が失敗して、バインドは一時停止状態に戻ります。

<a href="" id="send-and-receive-operations"></a>送信し、受信操作  
プロトコル ドライバーが送信を処理する必要があり、受信操作の実行では、および、一時停止中の状態します。 送信し、受信操作についての詳細についてを参照してください。[プロトコル ドライバーの送信と受信操作](protocol-driver-send-and-receive-operations.md)します。

<a href="" id="oid-requests"></a>OID 要求  
プロトコル ドライバーには、設定または基になるドライバーの情報をクエリする OID 要求を開始できます。 プロトコル ドライバーには、非連結と開始を除く、すべての状態から OID 要求を開始できます。

## <a name="related-topics"></a>関連トピック


[書き込み NDIS プロトコル ドライバー](writing-ndis-protocol-drivers.md)

 

 






