---
title: バス ドライバーでのデバイスの開始
description: バス ドライバーでのデバイスの開始
ms.assetid: 1babeabb-1866-4ca5-b5a3-380c246596e5
keywords:
- バス ドライバー WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18671be874293d10e008fc6870850bb360058103
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331954"
---
# <a name="starting-a-device-in-a-bus-driver"></a>バス ドライバーでのデバイスの開始





子のデバイスを起動するバス ドライバー (子*PDO*)、次のようなプロシージャを使ってその[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

1.  デバイスを起動します。

    正確な手順では、デバイスからデバイスが異なります。

    たとえば、PCI バス ドライバーは、PCI バス上の要求を有効にするには、そのマッピング レジスタをプログラムします。 PnP ISA バス ドライバーにより、関数のドライバーがアクセスできるように、PnP ISA カード。

2.  IRP を完了します。

    バス ドライバーの開始操作が成功した場合、ドライバーは設定**Irp -&gt;IoStatus.Status**ステータス\_成功と呼び出し[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343) IO の優先順位を指定する\_いいえ\_インクリメントします。 バス ドライバーのステータスを返します\_成功からその*DispatchPnP*ルーチン。

    バス ドライバーには、その開始操作中にエラーが発生すると、ドライバーが IRP の呼び出しではエラー状態を設定**IoCompleteRequest** IO と\_いいえ\_インクリメントし、そのからエラーを返します*DispatchPnP*ルーチン。

バス ドライバーには、デバイスを起動するまでに時間が必要とする場合、IRP を保留中のマークを付けるし、状態を返す\_保留します。

 

 




