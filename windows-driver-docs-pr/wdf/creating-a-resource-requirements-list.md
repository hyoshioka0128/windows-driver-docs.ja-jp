---
title: リソース要件リストの作成
description: リソース要件リストの作成
ms.assetid: 1254aa21-c64b-4c62-93dc-6758cef382f9
keywords:
- ハードウェアリソース WDK KMDF、リソース要件リストの作成
- リソース要件 WDK KMDF の一覧表示
- リソース要件の一覧 WDK KMDF, 作成
- リソース-必要条件-リストオブジェクト WDK KMDF
- フレームワークリソース-要件リストオブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52ec21b7f4325cff7e4f39620759cff429de8990
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845615"
---
# <a name="creating-a-resource-requirements-list"></a>リソース要件リストの作成


バスドライバーが子デバイスを検出すると、ドライバーはデバイスのリソース要件の一覧を作成します。 リスト内の各項目は、デバイスの[論理的な構成](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#ddk-logical-configurations-kg)です。

バス列挙中にドライバーによってデバイスが報告されると、フレームワークはドライバーの[*EvtDeviceResourceRequirementsQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)コールバック関数を呼び出します。 このコールバック関数は、空のリソース要件リストを表すリソース要件リストオブジェクトへのハンドルを受け取ります。

次の手順を実行して、リソース要件の一覧に情報を追加する必要があります。

-   空の論理構成を作成します。

    ドライバーが指定する論理構成ごとに、ドライバーは[**Wdfioresourcelistcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistcreate)を呼び出して、空の論理構成を作成する必要があります。

-   論理構成にリソース記述子を追加します。

    リソース記述子を論理構成に追加するには、ドライバーは、デバイスに必要なハードウェアリソースの種類ごとに次の操作を行う必要があります。

    1.  ドライバーで割り当てられた[**IO\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_descriptor)の構造体を入力します。これは、特定のリソースの有効な値の範囲を指定します。
    2.  [**Wdfioresourcelistappenddescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistappenddescriptor)または[**Wdfioresourcelistappenddescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistinsertdescriptor)を呼び出して、IO\_リソース\_記述子構造の内容を論理構成に追加します。

    デバイスがリソースの種類のインスタンスを複数使用する場合、リソースにアクセスするスタック内のすべてのドライバーは、リソースが追加される順序を認識している必要があります。 たとえば、デバイスで i/o ポートアドレスの2つの範囲が必要な場合、リソース記述子にアクセスするすべてのドライバーは、2つの範囲が論理構成に追加される順序を認識している必要があります。

-   リソース要件の一覧に論理構成を追加します。

    デバイスのリソース要件の一覧に論理構成を追加するには、ドライバーが[**WdfIoResourceRequirementsListAppendIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistappendioreslist)または[**WdfIoResourceRequirementsListInsertIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistinsertioreslist)を呼び出します。

    デバイスにリソースを割り当てると、PnP マネージャーは、リスト内の最初の論理構成の要件を照合しようとします。 その構成に必要なリソースが使用できない場合、PnP マネージャーは、使用可能なリソースの一覧にある次の構成と一致します。

    ドライバーが PnP 以外のデバイスをサポートしている場合は、通常、ドライバーは[**WdfIoResourceRequirementsListSetSlotNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistsetslotnumber)と[**WdfIoResourceRequirementsListSetInterfaceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistsetinterfacetype)も呼び出す必要があります。

ドライバーの[*EvtDeviceResourceRequirementsQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query) callback 関数がを返すと、フレームワークはリソース要件リストを PnP マネージャーに渡します。

 

 





