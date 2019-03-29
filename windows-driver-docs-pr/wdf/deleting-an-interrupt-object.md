---
title: 割り込みオブジェクトの削除
description: 割り込みオブジェクトの削除
ms.assetid: B72DA452-B22F-47CD-8C5D-E741F09F556E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7432fb4727fe0460b3ecfa3eaff927e1c7e1449c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571077"
---
# <a name="deleting-an-interrupt-object"></a>割り込みオブジェクトの削除


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、呼び出すことによって、割り込みオブジェクトを作成する場合[ **IWDFDevice3::CreateInterrupt**](https://msdn.microsoft.com/library/windows/hardware/hh451208)ドライバーは、割り込みオブジェクトを削除する必要はありません。 フレームワークは、割り込みオブジェクトは、framework デバイス オブジェクトの子オブジェクトでは自動的に割り込みオブジェクトを削除します。

フレームワークは、次の規則を使用します。

-   ドライバーを呼び出す場合[ **CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208)からその[ **OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)コールバック メソッド、フレームワークは、割り込みを削除します。オブジェクトから、ドライバーが返された後にその[ **OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439739)コールバック。

-   ドライバーを呼び出す場合[ **CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208)からその[ **OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)コールバック メソッド、フレームワークは、割り込みオブジェクトを削除します。デバイスが削除されたとき。

ドライバーを呼び出すことができます必要に応じて、 [ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)割り込みオブジェクトをいつでも削除します。 ドライバーは、外側の新しい割り込みオブジェクトを作成できないため[ **OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)または[ **OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/hh439734)、手動で削除した、フレームワークは、それを削除する前に、ドライバーは、オブジェクトを削除する必要がありますしない限り、オブジェクトを使用しない必要があります。

 

 





