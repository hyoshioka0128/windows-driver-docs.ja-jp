---
title: IRP の再利用
description: IRP の再利用
ms.assetid: 19b09cf8-b88d-4808-9af0-038d3d02dceb
keywords:
- Irp WDK のカーネルの再利用
- Irp WDK カーネルの再利用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb148bdc1b892d18a5a374fa60751baccf913550
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373389"
---
# <a name="reusing-irps"></a>IRP の再利用





ドライバーができる特定の状況で*再利用*Irp します。 ドライバーの作成に必要な Irp を保持するために使用されるメモリ バッファーのプールを割り当てることができます。

ドライバーは Irp が I/O マネージャーによって発行された再利用する必要があります試みません。 具体的には、ドライバーしようとしないでくださいによって作成された Irp を再利用、 [ **IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iomakeassociatedirp)、 [ **IoBuildSynchronousFsdRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)、 [ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)、または[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)ルーチン。

ドライバーは、次のように、作成した Irp を安全に再利用できます。

1.  ドライバーは、生のメモリとして IRP を割り当てる場合 (など、呼び出すことによって[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)) で初期化して[ **IoInitializeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeirp)、安全に呼び出すことができます**IoInitializeIrp**または[ **IoReuseIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp)メモリ バッファーの再初期化します。

2.  Microsoft Windows 2000 と以降のオペレーティング システム、ドライバーは IRP の作成を[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp) IRP を呼び出すことで再利用できる**IoReuseIrp**します。

3.  呼び出すことによってドライバーが IRP を割り当てる場合**IoAllocateIrp**で、 *ChargeQuota*パラメーターに設定**FALSE**、安全に使用できる**IoInitializeIrp** IRP の再初期化します。 ドライバーが Windows 98 で動作する必要があります]、[解決策としてこのメソッドを使用できます。 ドライバーが Windows 2000 および以降のオペレーティング システムに特化して設計には、前のメソッドを使用する必要があります。

 

 




