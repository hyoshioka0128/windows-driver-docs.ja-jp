---
title: 電源管理対象の I/O キューを使用します。
description: 電源管理対象の I/O キューを使用します。
ms.assetid: 271d55ef-d82e-4ffd-bf41-a602c42c3f0e
keywords:
- I/O は、WDK KMDF、電源管理対象のキューします。
- 電源管理対象の I/O キュー WDK KMDF
- Requeue 引数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40e964f09d464c0ee5d0c9140fa364be84ddc1ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557639"
---
# <a name="using-power-managed-io-queues"></a>電源管理対象の I/O キューを使用します。


キューがかどうかを指定できます、ドライバー、I/O キューを作成するとき*電源管理対象*します。 I/O 要求が電源管理対象のキューで利用できる場合は、フレームワークは、デバイスの作業 (D0) 状態にある場合にのみ、ドライバーを要求を配信します。 フレームワークはフレームワークがドライバーに電源管理対象のキューから配信されるすべての I/O 要求が完了、キャンセル、または延期するまでの作業状態のままにするデバイスを許可しません。

電源管理対象の I/O キューの詳細については、[の I/O キューの電源管理](power-management-for-i-o-queues.md)を参照してください。

## <a name="callback-functions-for-power-managed-queues"></a>Power-Managed キューのコールバック関数


ドライバーは、電源管理対象の I/O キューを使用している場合は、2 つの追加のコールバック関数を提供できます。

<a href="" id="---------evtiostop"></a>[*EvtIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541788)  
[ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)コールバック関数は、指定された I/O 要求の処理を停止します。 デバイスがその動作 (D0) 状態のままかが削除された、ときにフレームワークの I/O キューの*EvtIoStop*ドライバーがないすべての I/O 要求に対して 1 回のコールバック関数[完了](completing-i-o-requests.md)など、要求をドライバー[を所有する](request-ownership.md)があるものと[転送](forwarding-i-o-requests.md)I/O のターゲットにします。

<a href="" id="---------evtioresume"></a>[*EvtIoResume*](https://msdn.microsoft.com/library/windows/hardware/ff541779)  
[ *EvtIoResume* ](https://msdn.microsoft.com/library/windows/hardware/ff541779)コールバック関数が停止していた I/O 要求の処理を再開します。 フレームワークの I/O キューの*EvtIoResume*作業の状態、デバイスが返された後、キューからドライバーにコールバック関数の I/O の配信を再開するときに要求します。

たびに、フレームワーク ドライバーの[ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)コールバック関数は、関数は、通常[完了](completing-i-o-requests.md)または[キャンセル](canceling-i-o-requests.md)I/O要求、または呼び出し[ **WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)をフレームワークに、要求の所有権を返します。

これは省略可能ですが、一般を入力してください、 [ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)電源管理対象のキューのコールバック関数。 提供することで*EvtIoStop*時間が経過する前にお使いのデバイスや、システムが低電力状態に入ることを短縮するには、ドライバーが役立ちます。

指定しない場合[ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)フレームワークを電源管理対象のキューには、デバイス (またはシステム) を移動する前に、電源管理対象のキューからドライバーに配信されるすべての要求が完了するまでの操作を待機します。低電力状態またはデバイスを削除します。 可能性のある、これは、休止状態または別のシステム電源の状態に入るをシステムを防ぐことができます。 極端な場合、バグチェック コード 9F で、システムがクラッシュをしまうことができます。

安全に省略できますが、ドライバー、I/O ターゲットへの要求を転送しません、不特定の時点の要求を所持していない場合は、 [ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)電源管理対象のキュー。

## <a name="waiting-for-dispatcher-objects"></a>ディスパッチャー オブジェクトを待機しています


一般に、ドライバーは nonarbitrary スレッドのコンテキスト内で同期メカニズムとしてのディスパッチャー オブジェクトを使用する必要がありますのみです。

[要求ハンドラー](request-handlers.md)任意のスレッド コンテキストで実行すると、電源管理対象のキューの要求ハンドラーを待つ必要がありますいないカーネルのディスパッチャー オブジェクトを設定します。 そうと、デッドロックが発生する可能性があります。

ディスパッチャー オブジェクトでは、ドライバーが待機できる場合とできない場合の対処方法の詳細については、[カーネルのディスパッチャー オブジェクトの概要](https://msdn.microsoft.com/library/windows/hardware/ff548068)を参照してください。

 

 





