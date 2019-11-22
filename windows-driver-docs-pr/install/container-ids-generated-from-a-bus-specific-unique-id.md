---
title: バスに固有の一意の ID から生成されたコンテナー ID
description: バスに固有の一意の ID から生成されたコンテナー ID
ms.assetid: 06bd4f06-51f2-4983-9ddc-bff27eaa367e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60603d68d5354c42ecf79f573fb7025fed8f6013
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840650"
---
# <a name="container-ids-generated-from-a-bus-specific-unique-id"></a>バスに固有の一意の ID から生成されたコンテナー ID


デバイスのコンテナー ID を生成する方法としては、バス固有の一意の ID を使用することをお勧めします。 これは、コンテナー Id を生成するための最も正確で信頼性の高い方法です。

次の条件に該当する場合は、プラグアンドプレイ (PnP) マネージャーがこのメソッドを使用します。

-   デバイスには、バス固有の一意の ID が含まれています。

-   デバイスのバスドライバーは、この一意の ID を存在し、適切な形式として認識します。

-   バスドライバーは、一意の ID をグローバル一意識別子 (*GUID*) に確実にハッシュし、 [**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**QueryId**メンバーが**busquerycontainerid**に設定されている場合に[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)関数コードに応答してこの guid を返します。

Windows 7 以降のバージョンの Windows では、いくつかの一般的な種類のバスに対して受信トレイドライバーが提供されています。 これには、USB、Bluetooth、および PnP-X が含まれます。 これらのバスの種類では、デバイスにはバス固有の一意の ID を含める必要があります。 指定された Windows バスドライバーは、デバイスから一意の ID を読み取り、コンテナー ID を作成します。

次のトピックでは、受信トレイバスドライバーが特定の種類のバスのコンテナー Id を生成する方法について説明します。

[USB デバイスのコンテナー Id](container-ids-for-usb-devices.md)

[Bluetooth デバイスのコンテナー Id](container-ids-for-bluetooth-devices.md)

[PnP X デバイスのコンテナー Id](container-ids-for-pnp-x-devices.md)

[1394デバイスのコンテナー Id](container-ids-for-1394-devices.md)

[ESATA デバイスのコンテナー Id](container-ids-for-esata-devices.md)

[PCI Express デバイスのコンテナー Id](container-ids-for-pci-express-devices.md)

 

 





