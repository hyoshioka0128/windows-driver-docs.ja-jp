---
title: IRP の再利用
description: IRP の再利用
ms.assetid: 19b09cf8-b88d-4808-9af0-038d3d02dceb
keywords:
- Irp WDK カーネル、再利用
- Irp WDK カーネルの再利用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b75e052efd478013ff5d3c532e481ae1250acf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838448"
---
# <a name="reusing-irps"></a>IRP の再利用





特定の状況下では、ドライバーが irp を*再利用*できます。 ドライバーは、作成する必要がある Irp を保持するために使用するメモリバッファーのプールを割り当てることができます。

ドライバーは、i/o マネージャーによって発行された Irp を再利用しないようにする必要があります。 特に、ドライバーは、 [**IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)、 [**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)、 [**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)、または[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)ルーチンによって作成された irp を再利用しないようにする必要があります。

ドライバーは、次のように、作成した Irp を安全に再利用できます。

1.  ドライバーが IRP を生メモリとして割り当てる場合 (たとえば、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出して)、 [**IoIoReuseIrp eirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp)を使用して初期化すると、 **ioinitializeirp**または[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)を安全に呼び出して、メモリバッファーを再初期化できます。

2.  Microsoft Windows 2000 以降のオペレーティングシステムでは、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)を使用して irp を作成するドライバーは、 **IoReuseIrp**を呼び出すことによって、irp を再利用できます。

3.  *ChargeQuota*パラメーターを**FALSE**に設定して**ioallocateirp**を呼び出すことによってドライバーが irp を割り当てる場合、 **IO eirp**を使用して irp を再初期化することができます。 Windows 98/Me で動作する必要があるドライバーは、回避策としてこの方法を使用できます。 Windows 2000 以降のオペレーティングシステム用に厳密に設計されたドライバーでは、前の方法を使用する必要があります。

 

 




