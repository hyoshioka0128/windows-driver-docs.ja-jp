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
ms.openlocfilehash: 60c2d6269ffbd9fb8f5ce53d6ea25f581ef26a6d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362321"
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
*Detached*状態は、フィルター モジュールの初期状態です。 NDIS フィルター ドライバーを呼び出すことができますフィルター モジュールがこの状態のときは、 [ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)ドライバー スタックに、フィルター モジュールにアタッチします。 NDIS がフィルター ドライバーを呼び出すときに*FilterAttach*関数、フィルター モジュールは、アタッチ状態になります。 アタッチ操作が失敗した場合、フィルター モジュールをデタッチ ステートを返します。 呼び出し、モジュールの場合は、一時停止状態と NDIS、 [ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)関数は、モジュールは、デタッチされた状態に戻ります。

<a href="" id="attaching"></a>アタッチ  
フィルター モジュールの場合、*アタッチ*状態では、フィルター ドライバーはドライバー スタックにモジュールをアタッチする準備を行います。 フィルター モジュールの準備が完了した後、フィルター モジュールが一時停止状態になります。 (たとえば、必要なリソースを利用できません) ため、障害が発生した場合、フィルター モジュールは、デタッチの状態に戻ります。

<a href="" id="paused"></a>一時停止  
フィルター モジュールの場合、 *Paused*状態では、フィルター モジュールの送信を実行または受信操作はありません。 フィルター モジュールの場合、*アタッチ*状態と[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)が成功すると、フィルター モジュールが入力、 *Paused*状態。 フィルター モジュールの場合、*一時停止中*状態と、一時停止操作が完了する、フィルター モジュールが入力、 *Paused*状態。 フィルター モジュールの場合、 *Paused*状態および NDIS フィルター ドライバーを呼び出す[ **FilterRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff549962)関数の場合、フィルター モジュールが入力、*再開しています*状態。 フィルター モジュールの場合、 *Paused*状態 NDIS 呼び出しは、ドライバーの*FilterDetach*ハンドラー、フィルター モジュールが入力、 *Detached*状態。

<a href="" id="restarting"></a>再起動します。  
*再起動*状態では、フィルター ドライバーに送信を再起動し、受信フィルター モジュールの操作に必要なすべての操作が完了するとします。 フィルター モジュールが一時停止状態では、NDIS 呼び出してドライバーの*FilterRestart*関数、フィルター モジュールは、再開中状態になります。 再起動が失敗した場合、フィルター モジュールが一時停止状態に戻ります。 再起動が成功した場合は、フィルター モジュールが実行状態になります。

<a href="" id="running"></a>実行しています。  
*を実行している*状態では、フィルター ドライバーは、通常の送信を実行し、モジュールのフィルター処理を受信します。 フィルター モジュールが再起動状態と、ドライバーが送信を実行し、操作を受信する準備ができて、フィルター モジュールが実行状態になります。

<a href="" id="pausing"></a>一時停止  
*一時停止中*状態では、フィルター ドライバーに送信を停止し、受信フィルター モジュールの操作に必要なすべての操作が完了するとします。 すべて返す NDIS、その未処理を完了する要求を送信するすべてのフィルター ドライバーが待つ必要があります、未処理の受信表示します。 フィルター モジュールが実行中の状態では、NDIS 呼び出してドライバーの[ *FilterPause* ](https://msdn.microsoft.com/library/windows/hardware/ff549957)関数、フィルター モジュールは、一時停止状態になります。 フィルター ドライバーには、一時停止操作が失敗することはできません。 一時停止操作が完了したら、フィルター モジュールが一時停止状態になります。

## <a name="related-topics"></a>関連トピック


[ドライバー スタックの管理](driver-stack-management.md)

[NDIS フィルター ドライバー](ndis-filter-drivers.md)

 

 






