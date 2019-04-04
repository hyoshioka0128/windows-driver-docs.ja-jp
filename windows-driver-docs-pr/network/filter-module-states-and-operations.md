---
title: フィルター モジュールの状態と操作
description: フィルター モジュールの状態と操作
ms.assetid: b5798865-8332-477b-b155-79a3db6ff6fa
keywords:
- フィルター ドライバー WDK ネットワークの状態
- NDIS フィルター ドライバー WDK、状態
- WDK NDIS フィルターを状態します。
- デタッチされた状態の WDK ネットワーク
- 状態の WDK ネットワー キングのアタッチ
- WDK のネットワークを一時停止の状態
- WDK ネットワークの状態を再起動します。
- 実行状態の WDK ne
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95ea5eebc608b3bb5748cebc166cea444dc732ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580658"
---
# <a name="filter-module-states-and-operations"></a>フィルター モジュールの状態と操作





フィルター ドライバーは、ドライバーを管理する各フィルター モジュール (フィルター ドライバーのインスタンス) の次の操作の状態をサポートする必要があります。

<a href="" id="detached"></a>デタッチ  
*Detached*状態は、フィルター モジュールの初期状態です。 NDIS フィルター ドライバーを呼び出すことができますフィルター モジュールがこの状態のときは、 [ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)ドライバー スタックに、フィルター モジュールにアタッチします。

<a href="" id="attaching"></a>アタッチ  
*アタッチ*状態では、フィルター ドライバーはドライバー スタックに、フィルター モジュールをアタッチする準備を行います。

<a href="" id="paused"></a>一時停止  
*Paused*状態では、フィルター ドライバーの送信を実行または受信操作はありません。

<a href="" id="restarting"></a>再起動します。  
*再起動*状態では、フィルター ドライバーに送信を再起動し、受信フィルター モジュールの操作に必要なすべての操作が完了するとします。

<a href="" id="running"></a>実行しています。  
*を実行している*状態では、フィルター ドライバーは、通常の送信を実行し、モジュールのフィルター処理を受信します。

<a href="" id="pausing"></a>一時停止  
*一時停止中*状態では、フィルター ドライバーに送信を停止し、受信フィルター モジュールの操作に必要なすべての操作が完了するとします。

次の表では、見出しは、フィルター モジュールの状態です。 主なイベントは、最初の列に表示されます。 テーブル内のエントリの残りの部分は、[次へ] を指定状態フィルター モジュールが特定の状態でイベントが発生した後に入るようにします。 空のエントリは、無効なイベントの状態の組み合わせを表します。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント/状態</th>
<th align="left">Detached</th>
<th align="left">アタッチ</th>
<th align="left">一時停止</th>
<th align="left">再起動します。</th>
<th align="left">実行中</th>
<th align="left">一時停止</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>フィルターをアタッチします。</p></td>
<td align="left"><p>アタッチ</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>アタッチが完了しました</p></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>フィルターをデタッチします。</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Detached</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>再起動をフィルター処理します。</p></td>
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
<td align="left"><p>実行中</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>一時停止をフィルター処理します。</p></td>
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
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="even">
<td align="left"><p>アタッチに失敗しました</p></td>
<td align="left"></td>
<td align="left"><p>Detached</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>再起動に失敗しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>送受信</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OID 要求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"><p>再起動します。</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
</tbody>
</table>

 

プライマリ フィルター ドライバーのイベントの定義は次のとおりです。

<a href="" id="--------filter-attach--------"></a> フィルターをアタッチします。   
NDIS というドライバーの[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)ドライバー スタックにフィルター モジュールにアタッチします。 フィルター モジュールのインポートに関する詳細については、[フィルター モジュールのアタッチ](attaching-a-filter-module.md)を参照してください。

<a href="" id="attach-is-complete"></a>アタッチが完了しました  
フィルター モジュールの場合、*アタッチ*状態と、フィルター ドライバーは、フィルター モジュールに必要なリソース フィルター モジュールが入力したすべての初期化が完了すると、 *Paused*状態。

<a href="" id="--------filter-detach--------"></a> フィルターをデタッチします。   
NDIS というドライバーの[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)ドライバー スタックからフィルター モジュールをデタッチする関数。 詳細については、[フィルター モジュールをデタッチ](detaching-a-filter-module.md)を参照してください。

<a href="" id="--------filter-restart--------"></a> 再起動をフィルター処理します。   
NDIS というドライバーの[ *FilterRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff559435)関数を一時停止中のフィルター モジュールを再起動します。 詳細については、[フィルター モジュールの開始](starting-a-filter-module.md)を参照してください。

<a href="" id="restart-is-complete"></a>再起動が完了  
フィルター モジュールの場合、*再起動*状態と、ドライバーは、送信を実行し、操作を受信する準備が、フィルター モジュールが入力、*を実行している*状態。

<a href="" id="--------filter-pause--------"></a> 一時停止をフィルター処理します。   
NDIS というドライバーの[ *FilterPause* ](https://msdn.microsoft.com/library/windows/hardware/ff549957)フィルター モジュールを一時停止する関数。 詳細については、[フィルター モジュールを一時停止](pausing-a-filter-module.md)を参照してください。

<a href="" id="pause-is-complete"></a>一時停止が完了  
ドライバーの送信を停止し、受信操作に必要なすべての操作が完了した、一時停止操作が完了し、フィルター モジュールが、 *Paused*状態。

<a href="" id="attach-failed"></a>アタッチに失敗しました  
NDIS ドライバーの場合[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)関数と、アタッチ操作は、(たとえば、必要なリソースを利用できません) ために失敗した場合、フィルター モジュールを返す、 *デタッチされた*状態。

<a href="" id="restart-failed"></a>再起動に失敗しました  
NDIS ドライバーの場合[ *FilterRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff549962)関数と、再起動が失敗、フィルター モジュールを返します、 *Paused*状態。

<a href="" id="send-and-receive-operations"></a>送信し、受信操作  
ドライバーが送信を処理しでの操作を受け取ることができます、*を実行している*と*一時停止中*状態。 送信し、受信操作についての詳細についてを参照してください。[フィルター モジュールの送信と受信操作](filter-module-send-and-receive-operations.md)します。

<a href="" id="oid-requests"></a>OID 要求  
ドライバーは OID の要求を処理できる、*を実行している*、*再開中*、 *Paused*、および*一時停止中*状態。 OID 要求の詳細については、[フィルター モジュールの OID 要求](filter-module-oid-requests.md)を参照してください。

 

 





