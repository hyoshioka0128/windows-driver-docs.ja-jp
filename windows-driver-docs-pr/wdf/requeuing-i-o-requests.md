---
title: I/O 要求をキューに戻す
description: I/O 要求をキューに戻す
ms.assetid: b509959c-b2ab-4f04-9c08-5c5e90726b73
keywords:
- I/O 要求の WDK KMDF、requeuing
- requeuing I/O 要求の WDK KMDF
- 要求の処理の WDK KMDF、requeuing I/O 要求します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7971188e2320f3c9c830be575e14b404e6a5a25a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325209"
---
# <a name="requeuing-io-requests"></a>I/O 要求をキューに戻す





ドライバーは、I/O キューから取得する I/O 要求を入れることができます。 ドライバーは、ドライバーは、同じデバイスを作成した別の I/O キューの I/O 要求を入れることができます。 さらに、[バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540704)子デバイスの I/O キューから親デバイスの I/O キューへの I/O 要求を入れることができます。

### <a name="requeuing-an-io-request-to-a-different-io-queue-for-a-device"></a>デバイスの別の I/O キューの I/O 要求を requeuing

ドライバーの要求ハンドラーは、ドライバーの I/O キューからの I/O 要求を受け取る、ドライバーを呼び出すことが[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)別のキューに要求をキューに再登録します。

たとえば、要求の処理、ドライバーの前に、要求にリソースを割り当てることは、ドライバー [ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)コールバック関数のすべての要求を受信、ストアのリソースでした各要求のコンテキストのメモリ、および次の情報[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)するその他のキューへの各要求をキューに再登録します。

ドライバーを呼び出す場合[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958) requeue I/O に I/O から取得したドライバーがキューを要求を使用して、シーケンシャル[メソッドのディスパッチ](dispatching-methods-for-i-o-requests.md)、フレームワークは、次の I/O 要求から配信シーケンシャル キュー ドライバーにキューに再登録要求の完了を待たずにします。

呼び出すことができます、ドライバーは、手動のメソッドのディスパッチに使用されている場合、 [ **WdfRequestRequeue** ](https://msdn.microsoft.com/library/windows/hardware/ff550012)メソッドからのドライバーを取得、I/O キューの先頭に、I/O 要求を返します。 呼び出した後**WdfRequestRequeue**、ドライバーの次回の呼び出し[ **WdfIoQueueRetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548462)キューに再登録要求を取得します。

### <a name="requeuing-an-io-request-to-a-parent-devices-io-queue"></a>親デバイスの I/O キューへの I/O 要求を requeuing

親デバイスの機能のドライバーが果たすことができる、[バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540704)を[列挙](enumerating-the-devices-on-a-bus.md)親デバイスの子デバイスを作成および[物理デバイス オブジェクト](wdm-concepts-for-kmdf-drivers.md#device-stacks)(Pdo) の子デバイス。 このようなドライバーでは、親デバイスを扱う必要がある子デバイスの I/O 要求を受信できる場合があります。

たとえば、プロトコル バス (USB) などでは、通常接続された各デバイスに割り当てられているハードウェア リソースを制御します。 そのため、親のバスの機能のドライバーでは、通常それぞれの子デバイスの I/O 操作を処理します。 I/O マネージャーが I/O 要求を送信すると、[デバイス スタック](wdm-concepts-for-kmdf-drivers.md#device-stacks)子デバイスのいずれかの関数のドライバー、バスを I/O が要求を受信、子デバイスの I/O キューのいずれかでそのドライバー子デバイスの PDO を作成するためです。 ドライバーは、親のバスのデバイスのコンテキストでの I/O 要求を処理できますが、前に、子デバイスの I/O キューから親デバイスに属している I/O キューへの I/O 要求がキューを再登録する必要があります。

ドライバーを呼び出すことはできませんただし、 [ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)お子様のキューからの要求を親のキューに移動します。 I/O マネージャーは、親と子のデバイス用の別のデバイス スタックを作成するため、基になる WDM デバイス オブジェクト最初に親を表す 1 つの子デバイスを表す 1 つから変更してください。

KMDF のバージョン 1.9 に、ドライバーでした I/O して要求を送信子デバイスからその親にのみを作成する[リモートの I/O ターゲット](general-i-o-targets.md)、子デバイスのデバイスのスタックのサイズを増やすと、正しい WDM デバイス オブジェクトを指定します。

ドライバーを呼び出すことができます KMDF バージョン 1.9 以降、 [ **WdfPdoInitAllowForwardingRequestToParent** ](https://msdn.microsoft.com/library/windows/hardware/ff548789)デバイスと、呼び出しに子を作成する前に[ **WdfRequestForwardToParentDeviceIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549959)お子様の I/O キューから親キューへの要求をキューに再登録します。 ドライバーを使用している場合**WdfPdoInitAllowForwardingRequestToParent**と**WdfRequestForwardToParentDeviceIoQueue**フレームワークは、お子様のデバイスのスタック サイズが増加し、正しい WDM を割り当てますI/O 要求にデバイス オブジェクト。

 

 





