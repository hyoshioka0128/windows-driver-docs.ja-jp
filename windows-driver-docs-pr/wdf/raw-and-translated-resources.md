---
title: 未処理リソースと変換済みリソース
description: 未処理リソースと変換済みリソース
ms.assetid: dfc1376d-7a1a-421c-82ae-e183cac77ec8
keywords:
- ハードウェアリソース WDK KMDF、生のリソース
- リソースリスト WDK KMDF
- ハードウェアリソース WDK KMDF、翻訳されたリソース
- 翻訳済みリソース WDK KMDF
- 生のリソース WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47ce8fc6b68d736b09d888b38d678a936ee777d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842233"
---
# <a name="raw-and-translated-resources"></a>未処理リソースと変換済みリソース


ドライバーの[*Evtdeviceremoveaddedresources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)または[*Evtdeviceのハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数がリソースリストを受け取ると、2つのバージョンのリストが受信されます。 一方のバージョンはデバイスの*生リソース*を表し、もう1つはデバイスの変換された*リソース*を表します。 どちらのバージョンも、同じ順序で同じハードウェアリソースのセットを表します。

-   生リソースとは、デバイスが接続されているバスに対して相対的なアドレスによって識別されるリソースのことです。 通常、デバイスをプログラムするドライバーは、これらのアドレスをデバイスに提供します。

-   変換されたリソースとは、ドライバーがリソースにアクセスするために使用するシステムの物理アドレスによって識別されるリソースのことです。

PCI バスデバイス用のドライバーは、デバイスの*ベースアドレスレジスタ*(バー) に表示される順序で一覧表示されるリソースを受け取ります。 ただし、追加のリソース記述子が一覧にインターリーブされる可能性があります。これは、バーのインデックス*X*のリソースが、リソースリスト内の同じインデックス位置にあるリソースと一致しない可能性があるためです。

生リソースと変換されたリソースの詳細については、 [**CM\_PARTIAL\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)構造体のメンバーの説明を参照してください。

デバイスの変換されたリソースの一覧に、CM の**Type**メンバーを持つリソースが含まれている場合は\_\_リソース\_記述子の構造体が**CmResourceTypeMemory**に設定されている場合、そのリソースにアクセスするすべてのドライバーは、示し

-   ドライバーの[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数は、システムの物理アドレスをシステムの仮想アドレスにマップするために、 [**Mmmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)を呼び出す必要があります。
-   ドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数は、 [**Mmunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)を呼び出してアドレスをマップ解除する必要があります。

バス相対アドレスのマッピングの詳細については、「[バスの相対アドレスを仮想アドレスにマップする](https://docs.microsoft.com/windows-hardware/drivers/kernel/mapping-bus-relative-addresses-to-virtual-addresses)」を参照してください。

 

 





