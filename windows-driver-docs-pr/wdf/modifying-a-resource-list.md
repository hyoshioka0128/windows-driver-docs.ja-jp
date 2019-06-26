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
ms.openlocfilehash: 91db6519865b8118340c74b94d598077f1b3e3c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379673"
---
# <a name="modifying-a-resource-list"></a>リソース リストの変更


ドライバーが提供する場合、 [ *EvtDeviceFilterAddResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)コールバック関数も提供する、 [ *EvtDeviceRemoveAddedResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)コールバック関数。 *EvtDeviceRemoveAddedResources*コールバック関数には、リソースが削除されますが、 *EvtDeviceFilterAddResourceRequirements*コールバック関数が追加されるため、バス ドライバーは使用しませんします。

デバイスのリソースの一覧内のリソースの記述子を変更するには、ドライバーは、次のメソッドを呼び出す必要があります。

-   [**WdfCmResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfcmresourcelistgetcount)リソースの記述子の数を取得します。

-   [**WdfCmResourceListGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfcmresourcelistgetdescriptor)をリソース記述子へのアクセスを取得します。

-   [**WdfCmResourceListRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfcmresourcelistremove)と[ **WdfCmResourceListRemoveByDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfcmresourcelistremovebydescriptor)リソースの記述子を削除します。

ドライバーでは、リソースを削除した場合は、両方から削除にする必要があります、[生、翻訳したリソースの一覧](raw-and-translated-resources.md)します。

 

 





