---
title: 待機/ウェイク操作の概要
description: 待機/ウェイク操作の概要
ms.assetid: 63453f7e-f656-4efc-bb44-9e2cb0232270
keywords:
- 電源管理 WDK カーネル、ウェイクアップ機能
- 外部ウェイクアップシグナル WDK
- 復帰デバイス
- ウェイクアップ機能 WDK の電源管理
- デバイスのウェイクアップと WDK の電源管理
- IRP_MN_WAIT_WAKE
- 待機/ウェイク Irp WDK 電源管理、待機/ウェイク Irp について
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93cdffab6eb2907726146d891356f94b4fd6ce7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838521"
---
# <a name="overview-of-waitwake-operation"></a>待機/ウェイク操作の概要





オペレーティングシステムのウェイクアップメカニズムは、次の図に示すように動作します。

![irp\-\-待機\-ウェイク処理の概要を示す図](images/send-waitwake.png)

1.  システムとデバイスの状態が "稼働中" になっている間は、デバイスの電源ポリシー所有者が、ウェイクアップ用にデバイスを有効 ("設定") する必要があると判断します。 電源ポリシーの所有者は、その PDO[**に対して**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)、デバイススタック内のすべてのドライバーを通知するために、出力 irp (マイナーコード[**IRP\_\_待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) を要求します。 要求では、ポリシー所有者がコールバックルーチンを指定します ( [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンと同じではありません)。

2.  電源マネージャーは、i/o マネージャーを介して、IRP をデバイススタックの一番上に送信します。

3.  ドライバーは、 *Iocompletion*ルーチンを設定し、バスドライバーに到達するまで IRP を渡します。

4.  バスドライバーは、可能な場合は物理デバイスでウェイクアップを有効にし、保留中の IRP をマークします。 必要に応じて、その親の待機/ウェイク IRP も要求します。

5.  後で、外部ウェイクアップシグナルが到着します。

6.  バスドライバーは、 **IRP\_完了し\_待機\_スリープ状態**にします。

7.  I/o マネージャーは、ドライバーが IRP をスタックに渡したときに設定された*Iocompletion*ルーチンを呼び出します。

8.  I/o マネージャーは、IRP を要求したときに、ポリシー所有者によって設定されたコールバックルーチンを呼び出します。

**IRP\_\_WAIT\_WAKE**要求では、デバイスまたはシステムの電源の状態が変更されません。 デバイスでウェイクアップを有効にするだけです。そのため、デバイスが適切なスリープ状態になると、外部信号によってデバイス (および場合によってはシステム) が再開されます。

ウェイクアップシグナルが到着した場合、ドライバーの動作は、デバイスがシステムをスリープ解除するか、それともそれ自体をスリープ解除するかと同じです。 デバイスのウェイクアップが有効になっていて、システムがスリープ状態にあり、デバイスがデバイスをウェイクアップできる場合、デバイスはシステムを起動します。 デバイスでウェイクアップが有効になっていて、システムの状態が [稼働中] の場合は、デバイスのみが起動されます。

コンピューターとデバイスは設計によって異なるので、特に電源装置に関しては、サポートされているシステムとデバイスの電源の状態 (待機/ウェイクアップをサポートできる状態) は、すべてのハードウェア構成で同じではありません。 そのため、デバイスの電源ポリシーとすべてのバスドライバーを所有するドライバーは、実行されている個々の構成の機能に細心の注意を払う必要があります。 詳細については、「[デバイスがシステムをスリープ解除できるかどうかを判断](determining-whether-a-device-can-wake-the-system.md)する」を参照してください。

待機/ウェイク操作の詳細については、「[デバイスツリーを使用した待機/ウェイク irp のパスについ](understanding-the-path-of-wait-wake-irps-through-a-device-tree.md)て」および「[待機/ウェイク Irp 完了の概要](overview-of-wait-wake-irp-completion.md)」を参照してください。

 

 




