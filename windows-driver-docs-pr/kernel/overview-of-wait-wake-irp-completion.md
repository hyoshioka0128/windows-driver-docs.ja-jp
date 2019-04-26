---
title: 待機/ウェイク IRP 完了の概要
description: 待機/ウェイク IRP 完了の概要
ms.assetid: a5e09fda-f722-4335-8576-7b058b2f7a21
keywords:
- 電源管理の WDK カーネル、ウェイク アップ機能
- 外部ウェイク信号 WDK
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
- IRP_MN_WAIT_WAKE
- Irp WDK の電源管理のウェイク/待機の完了
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936b23454102a8fe20fffc79f4a0e279fe65cb50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352000"
---
# <a name="overview-of-waitwake-irp-completion"></a>待機/ウェイク IRP 完了の概要





待機/ウェイク IRP をウェイク アップの信号が到着すると完了します。 ウェイク アップ通知は、デバイスに固有ですは通常、デバイスの通常のサービス イベント。 たとえば、受信のリングは、スリープ状態のモデムがスリープ解除する場合があります。

次の図は、待機/ウェイク IRP の完了手順を示します。

![待機/ウェイク irp を完了するための手順](images/comp-waitwake.png)

シグナルが発生したときにコントロールをバス ドライバー、バスが、デバイスが起こさになっていることを検出する時点で再入力します。 バス ドライバー サービスの必要なイベントと呼び出し[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)を完了する、 [ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766) IRP の PDO をします。

I/O マネージャーを呼び出して、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン デバイス スタックの上位のドライバーによって設定します。 *IoCompletion*日常的なそのドライバー サービス、必要に応じてウェイク アップのシグナルと呼び出し**IoCompleteRequest** IRP を完了します。 I/O マネージャーを呼び出し続けます*IoCompletion*操作ルーチンは、すべてのドライバーが IRP を完了するまで、デバイス スタックをバックアップします。

その*IoCompletion* 、日常的な (1 つ以上の PDO を作成します)、1 つ以上の子デバイスを列挙し、このような 1 つ以上のデバイスからの待機またはスリープ解除要求を受け取ったドライバー送信する必要が自体待機/ウェイク再待機自体を arm に IRP/別の子でスリープを解除します。 詳細については、次を参照してください。[デバイス ツリーを通じて待機/ウェイク Irp のパスを理解する](understanding-the-path-of-wait-wake-irps-through-a-device-tree.md)します。

呼び出した後*IoCompletion* IRP が下位のスタックに渡されるときに、ドライバーによって設定ルーチンでは、I/O マネージャーが待機/ウェイク IRP が要求されたときに、電源ポリシーの所有者によって設定するコールバック ルーチンを呼び出します。 コールバック ルーチンでポリシー所有者は、デバイスを動作状態に戻すし、存在する場合、その子の pdo 保留中待機/ウェイクの IRP を完了する必要があります。

子の IRP の完了が原因でを呼び出す I/O マネージャー *IoCompletion*ルーチンは、子のデバイスのスタックのドライバーによって設定され、具合です。 最終的には、devnode で元待機/ウェイク IRP を開始したポリシー所有者には、そのデバイスには、ウェイク アップの信号がアサートされ、すべての保留中待機/ウェイク Irp を完了することが決定します。

 

 




