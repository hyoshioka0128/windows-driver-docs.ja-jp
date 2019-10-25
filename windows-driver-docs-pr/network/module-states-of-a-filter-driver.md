---
title: フィルター ドライバーのモジュールの状態
description: フィルター ドライバーのモジュールの状態
ms.assetid: 139679d6-d3dc-433b-a35a-eb1e5ed3cb33
keywords:
- フィルタードライバーの WDK ネットワーク、モジュールの状態
- NDIS フィルタードライバー WDK、モジュールの状態
- 'モジュールの状態: WDK ネットワーク'
- フィルターモジュール WDK ネットワーク、フィルタードライバーの状態
- フィルタードライバーの WDK ネットワーク、フィルターモジュール
- NDIS フィルタードライバー WDK、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e2db7d1bf09d1b75b1a1a2cbd884228354124d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844219"
---
# <a name="module-states-of-a-filter-driver"></a>フィルター ドライバーのモジュールの状態





[NDIS フィルタードライバー](ndis-filter-drivers.md)は、ドライバーが管理するフィルターモジュール (フィルタードライバーのインスタンス) ごとに次の動作状態をサポートする必要があります。

-   Detached

-   アタッチ

-   一時停止

-   再起動

-   Running

-   一時停止

次の図は、これらの状態間の関係を示しています。

![フィルターモジュールの状態を示す図](images/filterstate.png)

次の例では、フィルターモジュールの状態を定義します。

<a href="" id="detached"></a>デタッチ  
*デタッチ*された状態は、フィルターモジュールの初期状態です。 フィルターモジュールがこの状態になると、NDIS はフィルタードライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出して、フィルターモジュールをドライバースタックにアタッチできます。 NDIS がフィルタードライバーの*Filterattach*関数を呼び出すと、フィルターモジュールはアタッチ状態に入ります。 アタッチ操作が失敗した場合、フィルターモジュールはデタッチされた状態に戻ります。 モジュールが一時停止状態であり、NDIS が[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出すと、モジュールはデタッチされた状態に戻ります。

<a href="" id="attaching"></a>付ける  
フィルターモジュールが*アタッチ*状態の場合、フィルタードライバーはモジュールをドライバースタックにアタッチする準備をします。 フィルターモジュールの準備が完了すると、フィルターモジュールが一時停止状態になります。 (必要なリソースが使用できないなどの理由で) エラーが発生した場合、フィルターモジュールはデタッチされた状態に戻ります。

<a href="" id="paused"></a>中  
フィルターモジュールが*一時停止*状態の場合、フィルターモジュールは送信操作または受信操作を実行しません。 フィルターモジュールが*アタッチ*状態であり、 [*filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)が正常に実行されると、フィルターモジュールは*一時停止*状態になります。 フィルターモジュール*が一時停止中の状態で*、一時停止操作が完了すると、フィルターモジュールは*一時停止*状態になります。 フィルターモジュールが*一時停止*状態にあり、NDIS がフィルタードライバーの[**filterrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)関数を呼び出すと、フィルターモジュールは*再起動*状態になります。 フィルターモジュールが*一時停止*状態にあり、NDIS がドライバーの*filterdetach*ハンドラーを呼び出すと、フィルターモジュールは*デタッチ*された状態に入ります。

<a href="" id="restarting"></a>再起動  
*再起動*状態では、フィルタードライバーは、フィルターモジュールの送信操作および受信操作を再開するために必要なすべての操作を完了します。 フィルターモジュールが一時停止状態にあり、NDIS がドライバーの*Filterrestart*関数を呼び出すと、フィルターモジュールは再起動状態になります。 再起動に失敗した場合、フィルターモジュールは一時停止状態に戻ります。 再起動が成功した場合、フィルターモジュールは実行中の状態になります。

<a href="" id="running"></a>起動  
*実行*状態では、フィルタードライバーはフィルターモジュールに対して通常の送受信処理を実行します。 フィルターモジュールが再起動中の状態で、ドライバーが送信および受信操作を実行する準備ができたら、フィルターモジュールは実行中の状態になります。

<a href="" id="pausing"></a>一時停止  
*一時停止*状態では、フィルタードライバーは、フィルターモジュールの送信操作および受信操作を停止するために必要なすべての操作を完了します。 フィルタードライバーは、未処理のすべての送信要求が完了するまで待機し、NDIS がすべての未処理の受信通知を返すまで待機する必要があります。 フィルターモジュールが Running 状態で、NDIS がドライバーの[*Filterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)関数を呼び出すと、フィルターモジュールは一時停止中の状態になります。 フィルタードライバーは、一時停止操作を失敗することはできません。 一時停止操作が完了すると、フィルターモジュールは一時停止状態になります。

## <a name="related-topics"></a>関連トピック


[ドライバースタックの管理](driver-stack-management.md)

[NDIS フィルタードライバー](ndis-filter-drivers.md)

 

 






