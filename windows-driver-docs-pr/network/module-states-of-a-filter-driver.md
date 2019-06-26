---
title: フィルター ドライバーのモジュールの状態
description: フィルター ドライバーのモジュールの状態
ms.assetid: 139679d6-d3dc-433b-a35a-eb1e5ed3cb33
keywords:
- フィルター ドライバー WDK ネットワーク、モジュール状態
- NDIS フィルター ドライバー WDK、モジュールの状態
- WDK のネットワークの状態モジュール
- フィルター モジュールの WDK ネットワー キング、フィルター ドライバーの状態
- フィルター ドライバー WDK ネットワー キング、フィルター モジュール
- NDIS フィルター ドライバー WDK、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce1914b299f2d833d60efa318fa7e1c9ef620b3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378679"
---
# <a name="module-states-of-a-filter-driver"></a>フィルター ドライバーのモジュールの状態





[NDIS フィルター ドライバー](ndis-filter-drivers.md)ドライバーを管理する各フィルター モジュール (フィルター ドライバーのインスタンス) の次の操作の状態をサポートする必要があります。

-   Detached

-   アタッチ

-   一時停止

-   再起動します。

-   実行中

-   一時停止

次の図は、これらの状態間の関係を示します。

![フィルター モジュールの状態を示す図](images/filterstate.png)

次に、フィルター モジュールの状態を定義します。

<a href="" id="detached"></a>デタッチ  
*Detached*状態は、フィルター モジュールの初期状態です。 NDIS フィルター ドライバーを呼び出すことができますフィルター モジュールがこの状態のときは、 [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)ドライバー スタックに、フィルター モジュールにアタッチします。 NDIS がフィルター ドライバーを呼び出すときに*FilterAttach*関数、フィルター モジュールは、アタッチ状態になります。 アタッチ操作が失敗した場合、フィルター モジュールをデタッチ ステートを返します。 呼び出し、モジュールの場合は、一時停止状態と NDIS、 [ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)関数は、モジュールは、デタッチされた状態に戻ります。

<a href="" id="attaching"></a>アタッチ  
フィルター モジュールの場合、*アタッチ*状態では、フィルター ドライバーはドライバー スタックにモジュールをアタッチする準備を行います。 フィルター モジュールの準備が完了した後、フィルター モジュールが一時停止状態になります。 (たとえば、必要なリソースを利用できません) ため、障害が発生した場合、フィルター モジュールは、デタッチの状態に戻ります。

<a href="" id="paused"></a>一時停止  
フィルター モジュールの場合、 *Paused*状態では、フィルター モジュールの送信を実行または受信操作はありません。 フィルター モジュールの場合、*アタッチ*状態と[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)が成功すると、フィルター モジュールが入力、 *Paused*状態。 フィルター モジュールの場合、*一時停止中*状態と、一時停止操作が完了する、フィルター モジュールが入力、 *Paused*状態。 フィルター モジュールの場合、 *Paused*状態および NDIS フィルター ドライバーを呼び出す[ **FilterRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_restart)関数の場合、フィルター モジュールが入力、*再開しています*状態。 フィルター モジュールの場合、 *Paused*状態 NDIS 呼び出しは、ドライバーの*FilterDetach*ハンドラー、フィルター モジュールが入力、 *Detached*状態。

<a href="" id="restarting"></a>再起動します。  
*再起動*状態では、フィルター ドライバーに送信を再起動し、受信フィルター モジュールの操作に必要なすべての操作が完了するとします。 フィルター モジュールが一時停止状態では、NDIS 呼び出してドライバーの*FilterRestart*関数、フィルター モジュールは、再開中状態になります。 再起動が失敗した場合、フィルター モジュールが一時停止状態に戻ります。 再起動が成功した場合は、フィルター モジュールが実行状態になります。

<a href="" id="running"></a>実行しています。  
*を実行している*状態では、フィルター ドライバーは、通常の送信を実行し、モジュールのフィルター処理を受信します。 フィルター モジュールが再起動状態と、ドライバーが送信を実行し、操作を受信する準備ができて、フィルター モジュールが実行状態になります。

<a href="" id="pausing"></a>一時停止  
*一時停止中*状態では、フィルター ドライバーに送信を停止し、受信フィルター モジュールの操作に必要なすべての操作が完了するとします。 すべて返す NDIS、その未処理を完了する要求を送信するすべてのフィルター ドライバーが待つ必要があります、未処理の受信表示します。 フィルター モジュールが実行中の状態では、NDIS 呼び出してドライバーの[ *FilterPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)関数、フィルター モジュールは、一時停止状態になります。 フィルター ドライバーには、一時停止操作が失敗することはできません。 一時停止操作が完了したら、フィルター モジュールが一時停止状態になります。

## <a name="related-topics"></a>関連トピック


[ドライバー スタックの管理](driver-stack-management.md)

[NDIS フィルター ドライバー](ndis-filter-drivers.md)

 

 






