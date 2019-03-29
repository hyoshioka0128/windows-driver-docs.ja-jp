---
title: ミニポート アダプターの状態と操作
description: ミニポート アダプターの状態と操作
ms.assetid: b47e2cbe-9da3-4600-9afe-b082e60b87fb
keywords:
- ミニポート アダプタの WDK ネットワー キング、状態
- アダプターの WDK ネットワー キング、状態
- ミニポート アダプタの WDK ネットワー キング、操作
- アダプターの WDK ネットワー キング、操作
- 停止状態の WDK ネットワーク
- シャット ダウン状態の WDK ネットワーク
- WDK ne の状態を初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f5e566d2e491fba9d2d7018687465b5bbf526c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580697"
---
# <a name="miniport-adapter-states-and-operations"></a>ミニポート アダプターの状態と操作





管理アダプターごとに、NDIS 6.0 または以降のバージョンのミニポート ドライバーは、次の操作状態のセットをサポートする必要があります。

<a href="" id="halted"></a>(停止)  
中止状態は、すべてのアダプターの初期状態です。 NDIS ドライバーを呼び出すことができます、アダプターは、中止の状態が、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数アダプターを初期化します。

<a href="" id="shutdown"></a>シャット ダウン  
シャット ダウン状態でシステムのシャット ダウンと再起動を行う必要があります、システムでは、アダプターをもう一度使用する前にします。

<a href="" id="initializing"></a>初期化  
状態の場合では、ミニポート ドライバーは、アダプターを初期化するために必要なすべての操作を完了します。

<a href="" id="paused"></a>一時停止  
一時停止状態で、アダプターすれば、受信したネットワーク データを示すまたは送信要求を受け入れるはできません。

<a href="" id="restarting"></a>再起動します。  
再起動の状態では、ミニポート ドライバーは、送信を再起動し、受信アダプターの操作に必要なすべての操作を完了します。

<a href="" id="running"></a>実行しています。  
実行中の状態では、ミニポート ドライバーは、送信を実行し、受信アダプターの処理します。

<a href="" id="pausing"></a>一時停止  
一時停止中の状態では、ミニポート ドライバーは、送信を停止し、受信アダプターの操作に必要なすべての操作を完了します。

次の表では、見出しは、アダプターの状態です。 主なイベントは、最初の列に表示されます。 テーブル内のエントリの残りの部分は、[次へ] を指定、アダプターは特定の状態でイベントが発生した後の入力を状態します。 空のエントリは、無効なイベントの状態の組み合わせを表します。

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
<th align="left">(停止)</th>
<th align="left">シャットダウン</th>
<th align="left">初期化</th>
<th align="left">一時停止</th>
<th align="left">再起動します。</th>
<th align="left">実行中</th>
<th align="left">一時停止</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"><em>MiniportInitializeEx</em></a></p></td>
<td align="left"><p>初期化</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>初期化が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559449" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559449)"><em>MiniportShutdownEx</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>シャットダウン</p></td>
<td align="left"><p>シャットダウン</p></td>
<td align="left"><p>シャットダウン</p></td>
<td align="left"><p>シャットダウン</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559388" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559388)"><em>MiniportHaltEx</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(停止)</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559435" data-raw-source="[&lt;em&gt;MiniportRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559435)"><em>MiniportRestart</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>再起動します。</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>再起動が完了</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>実行中</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559418" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559418)"><em>MiniportPause</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>一時停止が完了</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="odd">
<td align="left"><p>初期化に失敗しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(停止)</p></td>
<td align="left"></td>
<td align="left"></td>
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
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"><p>再起動します。</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
</tbody>
</table>

 

**注**  上記の表に示したイベントは、NDIS 6.0 またはそれ以降のアダプターのプライマリのイベント。

 

**注**  リセット操作ではミニポート アダプターの動作状態には影響しません。 リセット操作が進行中はアダプターの状態を変更する可能性があります。 たとえば、NDIS は、進行中のリセット操作がある場合に、ドライバーの一時停止のハンドラーを呼び出すことができます。 この場合、ドライバーは、リセット、または要件は、各操作の実行中に任意の順序で一時停止操作を完了できます。 ドライバーが要求パケットの送信の失敗時に、リセット操作またはキューに置かれ、完全に保持できる後でもです。 上位のドライバーが中に一時停止操作を完了できないことを確認する必要がありますただし、その送信パケットが保留中です。

 

プライマリのミニポート ドライバーのイベントの定義は次のとおりです。

<a href="" id="miniportinitializeex"></a>MiniportInitializeEx  
NDIS というドライバーの[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)アダプターを初期化します。 アダプターの初期化の詳細については、次を参照してください。[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

<a href="" id="initialize-is-complete"></a>初期化が完了しました  
後[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)初期化操作が完了し、アダプターが一時停止状態に正常に返されます。

<a href="" id="miniportshutdownex"></a>MiniportShutdownEx  
NDIS というドライバーの[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)アダプターをシャット ダウンする関数。 詳細については、次を参照してください。[ミニポート アダプターのシャット ダウン](miniport-adapter-shutdown.md)します。

<a href="" id="miniporthaltex"></a>MiniportHaltEx  
NDIS というドライバーの[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)アダプターを停止する関数。 詳細については、次を参照してください。[ミニポート アダプターを停止する](halting-a-miniport-adapter.md)します。

<a href="" id="miniportrestart"></a>MiniportRestart  
NDIS というドライバーの[ **MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)関数を一時停止中のアダプターを再起動します。 アダプターは、初期化後に、一時停止状態ではであるために、このイベントはアダプターの初期化が完了した後、アダプターを開始するも必要です。 詳細については、次を参照してください。[アダプター開始](starting-an-adapter.md)します。

<a href="" id="restart-is-complete"></a>再起動が完了  
ドライバー準備ができたら送信を処理し、受信操作を再開する操作が完了し、アダプターが実行中の状態。

<a href="" id="miniportpause"></a>MiniportPause  
NDIS というドライバーの[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)アダプターを一時停止する関数。 詳細については、次を参照してください。[アダプターを一時停止](pausing-an-adapter.md)します。

<a href="" id="pause-is-complete"></a>一時停止が完了  
ドライバーに必要なすべての操作が完了した後操作の送受信を停止、一時停止操作が完了および、アダプターが一時停止状態にします。

**注**  NDIS を返すすべてのドライバーが待つ必要があります、未処理受信表示、一時停止操作が完了する前にします。

 

<a href="" id="initialize-failed"></a>初期化に失敗しました  
NDIS ドライバーの場合[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数と初期化失敗する場合、アダプターを中止状態に戻ります。

<a href="" id="restart-failed"></a>再起動に失敗しました  
NDIS ドライバーの場合[ **MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)関数と再起動の試行が失敗、一時停止状態のアダプターのままです。

<a href="" id="send-and-receive-operations"></a>送信し、受信操作  
ドライバーが送信を処理する必要があり、受信操作の実行では、および、一時停止中の状態します。 送信し、受信操作についての詳細についてを参照してください。[ミニポート ドライバーの送信と受信操作](miniport-driver-send-and-receive-operations.md)します。

<a href="" id="oid-requests"></a>OID 要求  
ドライバーは、実行中、再起動、一時停止、OID 要求を処理する必要があり、一時停止中の状態します。 OID 要求の詳細については、次を参照してください。[アダプターの OID 要求](miniport-adapter-oid-requests.md)します。

## <a name="related-topics"></a>関連トピック


[ミニポート アダプターを停止します。](halting-a-miniport-adapter.md)

[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)

[ミニポート アダプタのシャット ダウン](miniport-adapter-shutdown.md)

[ミニポート ドライバーの送信し、受信操作](miniport-driver-send-and-receive-operations.md)

[アダプターを一時停止](pausing-an-adapter.md)

[アダプターの開始](starting-an-adapter.md)

 

 






