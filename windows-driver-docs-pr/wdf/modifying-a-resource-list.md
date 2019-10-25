---
title: リソース リストの変更
description: リソース リストの変更
ms.assetid: 571b2990-5627-434e-b8fc-d2564188f544
keywords:
- ブート構成リソースの一覧 WDK KMDF、変更
- ハードウェアリソース WDK KMDF、リソースリスト
- リソースリスト WDK KMDF、変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6c491bdadc6f6cdb1984ad5471a507b0602f1b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843145"
---
# <a name="modifying-a-resource-list"></a>リソース リストの変更


ドライバーが[*EvtDeviceFilterAddResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)コールバック関数を提供する場合は、 [*Evtdeviceremoveaddedresources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)コールバック関数も提供する必要があります。 *Evtdeviceremoveaddedresources*コールバック関数は、 *EvtDeviceFilterAddResourceRequirements* callback 関数によって追加されたリソースを削除して、バスドライバーがそれを使用しないようにします。

デバイスのリソースリスト内のリソース記述子を変更するには、ドライバーは次のメソッドを呼び出す必要があります。

-   [**WdfCmResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetcount)。リソース記述子の数を取得します。

-   [**Wdfcmresourcelistgetdescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetdescriptor)。リソース記述子へのアクセス権を取得します。

-   [**Wdfcmresourcelistremove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistremove)および[**Wdfcmresourcelistremovebydescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistremovebydescriptor)。リソース記述子を削除します。

ドライバーがリソースを削除する場合は、[未加工のリソースリストと変換](raw-and-translated-resources.md)されたリソースリストの両方から削除する必要があります。

 

 





