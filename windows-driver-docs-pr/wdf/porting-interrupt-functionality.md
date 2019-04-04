---
title: 割り込みの移植
description: 割り込みの移植
ms.assetid: E91B971D-044C-45A4-AD76-44AFB1213F8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1642864a7816681ceecc8d4ab044dfd06b78dc09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553980"
---
# <a name="porting-interrupts"></a>割り込みの移植


サポートしていると、割り込みのコードは、WDF と WDM ドライバーと似ています。 1 つの主な違いがあります。

-   WDF ドライバー WDFINTERRUPT オブジェクトを作成し、呼び出すことによって、割り込みサービス ルーチン (ISR) のコールバックを登録します[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)からその[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック。
-   WDM ドライバーが KINTERRUPT 構造を作成し、接続中に[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)処理します。

[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735) WDF ドライバーでのコールバック WDM ドライバーのと同じタスクを実行する[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)ルーチン。 *EvtInterruptIsr*コールバック呼び出し[ **WdfInterruptQueueDpcForIsr** ](https://msdn.microsoft.com/library/windows/hardware/ff547371)キューに、 [ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)ディスパッチに後で処理するためのコールバック\_レベル。 応答では、フレームワークは、このコールバックを実行しているシステム キューに DPC オブジェクトを追加します。

フレームワークの割り込みのオブジェクトの詳細については、[ハードウェアの割り込み処理](handling-hardware-interrupts.md)を参照してください。

 

 





