---
title: Raw と翻訳されたリソース
description: Raw と翻訳されたリソース
ms.assetid: dfc1376d-7a1a-421c-82ae-e183cac77ec8
keywords:
- ハードウェア リソース WDK KMDF、生のリソース
- リソースには、WDK KMDF が一覧表示されます。
- ハードウェア リソース WDK KMDF、翻訳済みのリソース
- WDK KMDF 翻訳済みのリソース
- WDK KMDF 生のリソース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d608551898ea3ce4cce0756ec06010418b0a937
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558574"
---
# <a name="raw-and-translated-resources"></a>Raw と翻訳されたリソース


ときに、ドライバーの[ *EvtDeviceRemoveAddedResources* ](https://msdn.microsoft.com/library/windows/hardware/ff540892)または[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数は、リソースを受け取ります。一覧で、2 つのバージョンの一覧を受け取ります。 1 つのバージョンは、デバイスを表します*生のリソース*、デバイスの他の表し*リソースを翻訳*します。 両方のバージョンでは、同じ順序で、ハードウェア リソースの同じセットを表します。

-   生のリソースは、デバイスが接続されているバスは、アドレスによって識別されるリソースです。 通常、プログラム、デバイス ドライバーは、デバイスにこれらのアドレスを提供します。

-   翻訳されたリソースは、リソースにアクセスするドライバーを使用して、システムの物理アドレスによって識別されるリソースです。

PCI バス デバイス用のドライバーがデバイスの表示される順序で記載されているリソースを受け取る*ベース アドレスを登録*(棒)。 ただし、記述子の追加のリソースを一覧で、インターリーブされる場合がありますようにインデックス位置にあるリソース*X*バーに必ずしも一致しないリソースの一覧で、同じインデックス位置にあるリソース。

Raw と翻訳されたリソースの詳細については、のメンバーの説明を参照してください、 [ **CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)構造体。

リソースの一覧にはで、リソースが含まれています、デバイスの変換された場合、**型**、CM のメンバー\_部分\_リソース\_記述子構造体を設定**CmResourceTypeMemory**、そのリソースにアクセスするすべてのドライバーは、次を実行する必要があります。

-   ドライバーの[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数を呼び出す必要があります[ **MmMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff554618)システムの物理アドレスにマップするにはシステムの仮想アドレス。
-   ドライバーの[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数を呼び出す必要があります[ **MmUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff556387)アドレスの割り当てを解除します。

バスの相対アドレスのマッピングの詳細については、次を参照してください。[マッピング Bus 相対アドレスを仮想アドレス](https://msdn.microsoft.com/library/windows/hardware/ff554399)します。

 

 





