---
title: バス ドライバーでのデバイスの開始
description: バス ドライバーでのデバイスの開始
ms.assetid: 1babeabb-1866-4ca5-b5a3-380c246596e5
keywords:
- バスドライバー WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2719ef400061892af5df236cd64880f87f25bac2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838413"
---
# <a name="starting-a-device-in-a-bus-driver"></a>バス ドライバーでのデバイスの開始





バスドライバーは、子デバイス (子*PDO*) を起動します。その際、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで次のような手順を実行します。

1.  デバイスを起動します。

    正確な手順は、デバイスによって異なります。

    たとえば、pci バスドライバープログラムは、PCI バス上の要求を有効にするために、そのマッピングを登録します。 PnP isa バスドライバーは、関数ドライバーがアクセスできるように、PnP ISA カードを有効にします。

2.  IRP を完了します。

    バスドライバーの開始操作が成功した場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定し、IO\_\_priority boost を指定して[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。 バスドライバーは、 *DispatchPnP*ルーチンから STATUS\_SUCCESS を返します。

    バスドライバーが開始操作中にエラーを検出した場合、ドライバーは IRP にエラー状態を設定し、 **IoCompleteRequest**を呼び出して IO\_\_インクリメントを呼び出し、その*DispatchPnP*ルーチンからエラーを返します。

バスドライバーによってデバイスの起動に時間がかかる場合は、IRP を保留中としてマークし、状態\_保留中としてマークできます。

 

 




