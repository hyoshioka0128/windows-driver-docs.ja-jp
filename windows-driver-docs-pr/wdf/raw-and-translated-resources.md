---
title: 未処理リソースと変換済みリソース
description: 未処理リソースと変換済みリソース
ms.assetid: dfc1376d-7a1a-421c-82ae-e183cac77ec8
keywords:
- ハードウェア リソース WDK KMDF、生のリソース
- リソースには、WDK KMDF が一覧表示されます。
- ハードウェア リソース WDK KMDF、翻訳済みのリソース
- WDK KMDF 翻訳済みのリソース
- WDK KMDF 生のリソース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d670968e08cdbae0e5dc5699bc987fcb0dc221c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376306"
---
# <a name="raw-and-translated-resources"></a>未処理リソースと変換済みリソース


ときに、ドライバーの[ *EvtDeviceRemoveAddedResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)または[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数は、リソースを受け取ります。一覧で、2 つのバージョンの一覧を受け取ります。 1 つのバージョンは、デバイスを表します*生のリソース*、デバイスの他の表し*リソースを翻訳*します。 両方のバージョンでは、同じ順序で、ハードウェア リソースの同じセットを表します。

-   生のリソースは、デバイスが接続されているバスは、アドレスによって識別されるリソースです。 通常、プログラム、デバイス ドライバーは、デバイスにこれらのアドレスを提供します。

-   翻訳されたリソースは、リソースにアクセスするドライバーを使用して、システムの物理アドレスによって識別されるリソースです。

PCI バス デバイス用のドライバーがデバイスの表示される順序で記載されているリソースを受け取る*ベース アドレスを登録*(棒)。 ただし、記述子の追加のリソースを一覧で、インターリーブされる場合がありますようにインデックス位置にあるリソース*X*バーに必ずしも一致しないリソースの一覧で、同じインデックス位置にあるリソース。

Raw と翻訳されたリソースの詳細については、のメンバーの説明を参照してください、 [ **CM\_部分\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_partial_resource_descriptor)構造体。

リソースの一覧にはで、リソースが含まれています、デバイスの変換された場合、**型**、CM のメンバー\_部分\_リソース\_記述子構造体を設定**CmResourceTypeMemory**、そのリソースにアクセスするすべてのドライバーは、次を実行する必要があります。

-   ドライバーの[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数を呼び出す必要があります[ **MmMapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace)システムの物理アドレスにマップするにはシステムの仮想アドレス。
-   ドライバーの[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数を呼び出す必要があります[ **MmUnmapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)アドレスの割り当てを解除します。

バスの相対アドレスのマッピングの詳細については、次を参照してください。[マッピング Bus 相対アドレスを仮想アドレス](https://docs.microsoft.com/windows-hardware/drivers/kernel/mapping-bus-relative-addresses-to-virtual-addresses)します。

 

 





