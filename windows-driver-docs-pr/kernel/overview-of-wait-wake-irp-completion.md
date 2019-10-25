---
title: 待機/ウェイク IRP 完了の概要
description: 待機/ウェイク IRP 完了の概要
ms.assetid: a5e09fda-f722-4335-8576-7b058b2f7a21
keywords:
- 電源管理 WDK カーネル、ウェイクアップ機能
- 外部ウェイクアップシグナル WDK
- 復帰デバイス
- ウェイクアップ機能 WDK の電源管理
- デバイスのウェイクアップと WDK の電源管理
- IRP_MN_WAIT_WAKE
- 待機/ウェイク Irp WDK 電源管理、完了
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85da38055708b5f8b16dd7f0cc9ffae6a7393a7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827726"
---
# <a name="overview-of-waitwake-irp-completion"></a>待機/ウェイク IRP 完了の概要





ウェイクアップシグナルが到着すると、待機/ウェイク IRP が完了します。 ウェイクアップ信号はデバイス固有ですが、通常はデバイスの通常のサービスイベントです。 たとえば、着信音によって、スリープ状態のモデムがスリープ解除される場合があります。

次の図は、待機/ウェイク IRP を完了する手順を示しています。

![待機/ウェイク irp を完了するための手順](images/comp-waitwake.png)

シグナルが発生すると、デバイスがスリープ状態になったことをバスが検出した時点で、制御がバスドライバーに再入力されます。 バスドライバーは、必要に応じてイベントを処理し、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して\_irp を完了します。これにより、PDO に[ **\_WAKE IRP\_待機**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)ます。

次に、i/o マネージャーは、デバイススタック内の次の上位のドライバーによって設定された[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを呼び出します。 *Iocompletion*ルーチンでは、そのドライバーは必要に応じてウェイクアップシグナルを処理し、 **IoCompleteRequest**を呼び出して IRP を完了します。 I/o マネージャーは引き続き*Iocompletion*ルーチンを呼び出し、すべてのドライバーが IRP を完了するまで、デバイススタックをバックアップします。

*Iocompletion*ルーチンでは、複数の子デバイス (複数の PDO を作成) を列挙し、複数のデバイスから受信した待機/ウェイク要求を受け取るドライバーは、別の子の待機/ウェイクのために、待機/ウェイク IRP を再起動する必要があります. 詳細については、「[デバイスツリーを使用した待機/ウェイク irp のパスについ](understanding-the-path-of-wait-wake-irps-through-a-device-tree.md)て」を参照してください。

ドライバーによって設定された*Iocompletion*ルーチンがスタックに渡されたときに、そのルーチンを呼び出した後、i/o マネージャーは、待機/ウェイク IRP を要求したときに、電源ポリシー所有者によって設定されたコールバックルーチンを呼び出します。 コールバックルーチンでは、ポリシーの所有者がそのデバイスを動作中の状態に戻し、子の PDO (存在する場合) に対して保留中の待機/ウェイク IRP を完了する必要があります。

子の IRP を完了すると、i/o マネージャーは、子のデバイススタック内のドライバーによって設定された*Iocompletion*ルーチンを呼び出すようになります。 最終的には、devnode で元の待機/ウェイク IRP を開始したポリシー所有者が、デバイスがウェイクアップシグナルをアサートしたこと、および保留中の待機/ウェイク Irp がすべて完了したと判断します。

 

 




