---
title: Irp を再利用
description: Irp を再利用
ms.assetid: 19b09cf8-b88d-4808-9af0-038d3d02dceb
keywords:
- Irp WDK のカーネルの再利用
- Irp WDK カーネルの再利用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0277d837767c058bb7fe6eb50c1234f28967f3d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551124"
---
# <a name="reusing-irps"></a>Irp を再利用





ドライバーができる特定の状況で*再利用*Irp します。 ドライバーの作成に必要な Irp を保持するために使用されるメモリ バッファーのプールを割り当てることができます。

ドライバーは Irp が I/O マネージャーによって発行された再利用する必要があります試みません。 具体的には、ドライバーしようとしないでくださいによって作成された Irp を再利用、 [ **IoMakeAssociatedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549397)、 [ **IoBuildSynchronousFsdRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548330)、 [ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)、または[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)ルーチン。

ドライバーは、次のように、作成した Irp を安全に再利用できます。

1.  ドライバーは、生のメモリとして IRP を割り当てる場合 (など、呼び出すことによって[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)) で初期化して[ **IoInitializeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549315)、安全に呼び出すことができます**IoInitializeIrp**または[ **IoReuseIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549661)メモリ バッファーの再初期化します。

2.  Microsoft Windows 2000 と以降のオペレーティング システム、ドライバーは IRP の作成を[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257) IRP を呼び出すことで再利用できる**IoReuseIrp**します。

3.  呼び出すことによってドライバーが IRP を割り当てる場合**IoAllocateIrp**で、 *ChargeQuota*パラメーターに設定**FALSE**、安全に使用できる**IoInitializeIrp** IRP の再初期化します。 ドライバーが Windows 98 で動作する必要があります]、[解決策としてこのメソッドを使用できます。 ドライバーが Windows 2000 および以降のオペレーティング システムに特化して設計には、前のメソッドを使用する必要があります。

 

 




