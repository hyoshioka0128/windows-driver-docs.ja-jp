---
title: リソース リストの変更
description: リソース リストの変更
ms.assetid: 571b2990-5627-434e-b8fc-d2564188f544
keywords:
- ブート構成のリソースには、WDK KMDF、変更が一覧表示されます。
- ハードウェア リソース WDK KMDF、リソースを一覧表示します。
- リソースは、WDK KMDF、変更を一覧表示されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36fd23b5121d5fb895ca3092dd4f79b7c4a19722
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390163"
---
# <a name="modifying-a-resource-list"></a>リソース リストの変更


ドライバーが提供する場合、 [ *EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870)コールバック関数も提供する、 [ *EvtDeviceRemoveAddedResources*](https://msdn.microsoft.com/library/windows/hardware/ff540892)コールバック関数。 *EvtDeviceRemoveAddedResources*コールバック関数には、リソースが削除されますが、 *EvtDeviceFilterAddResourceRequirements*コールバック関数が追加されるため、バス ドライバーは使用しませんします。

デバイスのリソースの一覧内のリソースの記述子を変更するには、ドライバーは、次のメソッドを呼び出す必要があります。

-   [**WdfCmResourceListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff545687)リソースの記述子の数を取得します。

-   [**WdfCmResourceListGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff545688)をリソース記述子へのアクセスを取得します。

-   [**WdfCmResourceListRemove** ](https://msdn.microsoft.com/library/windows/hardware/ff545704)と[ **WdfCmResourceListRemoveByDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff545717)リソースの記述子を削除します。

ドライバーでは、リソースを削除した場合は、両方から削除にする必要があります、[生、翻訳したリソースの一覧](raw-and-translated-resources.md)します。

 

 





