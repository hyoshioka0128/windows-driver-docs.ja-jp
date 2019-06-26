---
title: リソース要件リストの作成
description: リソース要件リストの作成
ms.assetid: 1254aa21-c64b-4c62-93dc-6758cef382f9
keywords:
- ハードウェア リソース WDK KMDF、リソース要件のリストを作成します。
- WDK KMDF リソース要件の一覧
- リソース要件の一覧を作成する、WDK KMDF
- リソース要件のリスト オブジェクト WDK KMDF
- フレームワーク リソース要件リスト オブジェクトの WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 211fccf32acb4b726d0d52a27e9ba225790a01cc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382401"
---
# <a name="creating-a-resource-requirements-list"></a>リソース要件リストの作成


バス ドライバーでは、子デバイスを検出すると、ドライバーは、デバイスのリソース要件の一覧を作成する責任を負います。 リスト内の各項目は、[論理構成](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#ddk-logical-configurations-kg)デバイス。

ドライバーは、バスの列挙中にデバイスを報告、フレームワークのドライバーの[ *EvtDeviceResourceRequirementsQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)コールバック関数。 このコールバック関数では、空のリソースの要件リストを表すリソース要件のリスト オブジェクトを識別するハンドルを受け取ります。

ドライバーは、リソース要件の一覧に情報を追加するには、次を実行しする必要があります。

-   空の論理構成を作成します。

    呼び出す必要があります、ドライバー、ドライバーが指定する各論理構成[ **WdfIoResourceListCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistcreate)空の論理構成を作成します。

-   論理構成には、リソースの記述子を追加します。

    リソースの記述子を論理構成を追加するには、ドライバーは、デバイスが必要なハードウェア リソースの種類ごとに、次を行う必要があります。

    1.  ドライバーによって割り当てられた入力[ **IO\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_resource_descriptor)構造体は、特定のリソースの有効な値の範囲を指定します。
    2.  呼び出す[ **WdfIoResourceListAppendDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistappenddescriptor)または[ **WdfIoResourceListInsertDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistinsertdescriptor) IOの内容を追加するには\_リソース\_論理構成記述子構造体。

    デバイスは、リソースの種類の 1 つ以上のインスタンスを使用している場合、リソースへのアクセス、スタック内のすべてのドライバーはリソースを追加する順序に注意してくださいである必要があります。 たとえば、デバイスには、2 つの I/O ポートのアドレスの範囲が必要とする場合リソース記述子にアクセスするすべてのドライバーは論理構成に、2 つの範囲を追加する順序に注意してくださいである必要があります。

-   リソース要件の一覧には、論理構成を追加します。

    論理構成をデバイスのリソース要件の一覧、ドライバーの呼び出しを追加する[ **WdfIoResourceRequirementsListAppendIoResList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistappendioreslist)または[ **WdfIoResourceRequirementsListInsertIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistinsertioreslist)します。

    リソースをデバイスに割り当てるときに、PnP マネージャーは、一覧の最初の論理構成の要件を満たしてしようとします。 その構成に必要なリソースが利用できない場合、PnP マネージャーは次の構成を対象のリソースが使用可能な一覧と一致します。

    ドライバーは、非 PnP デバイスをサポートする場合、ドライバー通常呼び出す必要がありますも[ **WdfIoResourceRequirementsListSetSlotNumber** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistsetslotnumber)と[ **WdfIoResourceRequirementsListSetInterfaceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistsetinterfacetype)します。

ドライバーの後に[ *EvtDeviceResourceRequirementsQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)コールバック関数が返す、フレームワーク、リソース要件の一覧を渡します PnP マネージャー。

 

 





