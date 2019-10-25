---
title: ハードウェア リソースの概要
description: ハードウェア リソースの概要
ms.assetid: 34350031-daae-4213-b157-086a7a55e05b
keywords:
- ブート構成 WDK KMDF
- 論理構成 WDK KMDF
- ハードウェアリソース WDK KMDF、ハードウェアリソースについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 566f7896f3947d6359fe3a2e9917da8d4a6597b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843039"
---
# <a name="introduction-to-hardware-resources"></a>ハードウェア リソースの概要


ユーザーが PnP デバイスに接続した後、デバイスを[列挙](enumerating-the-devices-on-a-bus.md)するドライバーは通常、1つまたは複数の[論理構成](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#ddk-logical-configurations-kg)を作成します。これは、デバイスが使用できるハードウェアリソースの組み合わせです。 次のような構成があります。

-   システムの起動時にデバイスが必要とするハードウェアリソースの一覧を示す*ブート構成*。 (PnP デバイスの場合、この情報は BIOS によって提供されます)。

-   デバイスが動作できる追加の構成。 ドライバーは、これらの追加の構成を[リソース要件の一覧](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)にグループ化します。 PnP マネージャは、最終的にこの一覧からリソースを選択してデバイスに割り当てます。

ドライバーは、論理構成を作成した後、それらをフレームワークに送信し、フレームワークが PnP マネージャーに送信します。

次に、PnP マネージャーは、デバイスが必要とするドライバーを決定し、まだ読み込まれていない場合は読み込みます。 PnP マネージャーは、デバイスのハードウェア要件リストを確認のためにデバイスのドライバーに送信します。 関数ドライバーとフィルタードライバーは、この一覧を変更して、PnP マネージャーに送り返すことができます。

PnP マネージャーは、変更されたハードウェア要件の一覧を調べ、指定されたリソースがシステムで実際に使用可能であるかどうかを判断します。 PnP マネージャーによって以前に別のデバイスに割り当てられたリソースが必要な場合は、PnP マネージャーがシステムのデバイス間でリソースの再[配布](handling-requests-to-stop-a-device.md#redistributing-resources)を試みることがあります。

次に、PnP マネージャーは、PnP マネージャーがデバイスに割り当てるリソースの一覧である[リソースリスト](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)を作成します。 PnP マネージャーは、このリストを確認のためにデバイスのドライバーに送信します。 この時点で、関数とフィルタードライバーはリストからリソースを削除できますが、リソースを追加することはできません。

最後に、PnP マネージャーによってデバイスにリソースが割り当てられます。 フレームワークは、デバイスの機能とフィルタードライバーにリソースリストを渡し、デバイスとドライバーがリソースにアクセスできるようにするために必要な初期化をデバイスの関数ドライバーが実行します。

次の手順では、プロセスについてさらに詳しく説明します。

1.  [ユーザーはデバイスに](a-user-plugs-in-a-device.md)接続します。

2.  バスドライバーは、デバイスを検出し、それを[列挙](enumerating-the-devices-on-a-bus.md)します。

3.  このフレームワークは、バスドライバーの[*EvtDeviceResourcesQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query) callback 関数を呼び出します。これにより、デバイスのブート構成を記述する[リソースリストが作成さ](creating-a-resource-list-for-a-boot-configuration.md)れます。

4.  このフレームワークは、バスドライバーの[*EvtDeviceResourceRequirementsQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query) callback 関数を呼び出します。これにより、デバイスの[リソース要件の一覧が作成さ](creating-a-resource-requirements-list.md)れます。

5.  PnP マネージャは、デバイスが必要とするドライバを特定し、それらがまだ読み込まれていない場合はデバイスのドライバスタックを作成します。

6.  PnP マネージャーは、確認のためにデバイスのリソース要件の一覧をドライバースタックに送信します。 リストがドライバースタックの下に移動すると、フレームワークは各関数とフィルタードライバーの[*EvtDeviceFilterRemoveResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) callback 関数を呼び出します。 リストがスタックをさかのぼっていくにつれて、フレームワークは各関数とフィルタードライバーの[*EvtDeviceFilterAddResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) callback 関数を呼び出します。 これらのコールバック関数は[、どちらもリソース要件の一覧を変更](modifying-a-resource-requirements-list.md)できます。

7.  PnP マネージャーは、デバイスのリソースリストを作成し、それを確認のためにドライバースタックに送信します。 フレームワークは、各関数とフィルタードライバーの[*Evtdeviceremoveaddedresources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)コールバック関数を呼び出します。これにより、ドライバーの*EvtDeviceFilterAddResourceRequirements* callback 関数によって追加されたリソースが、バスによって[削除](modifying-a-resource-list.md)されます。ドライバーは、ドライバーの使用を試みません。

8.  このフレームワークは、PnP マネージャーから最終的なリソースリストを受け取り、それを格納します。

9.  ドライバーが[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)を呼び出して割り込みオブジェクトを作成する場合、フレームワークはリソースリスト内の割り込みリソースを検出し、それらを interrupt オブジェクトに割り当てます。

10. デバイスが初期化されていない D0 状態になった後、フレームワークは、デバイスのリソースリストの[未加工および翻訳](raw-and-translated-resources.md)されたバージョンを入力引数として渡して、各ドライバーの[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数を呼び出します。 ドライバーはリソースリストを保存できます。これは、フレームワークがドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数を呼び出すまで有効です。

 

 





