---
title: バスに固有の一意の ID から生成されたコンテナー ID
description: バスに固有の一意の ID から生成されたコンテナー ID
ms.assetid: 06bd4f06-51f2-4983-9ddc-bff27eaa367e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a82c584ae4cf3c09b427f1b80bde8c677b26af4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356334"
---
# <a name="container-ids-generated-from-a-bus-specific-unique-id"></a>バスに固有の一意の ID から生成されたコンテナー ID


デバイスがバスに固有の一意の ID に基づいて、コンテナー ID を生成することをお勧め これは、コンテナー id が生成する最も正確で信頼性の高い方法です。

プラグ アンド プレイ (PnP) マネージャーが、次に該当する場合、このメソッドを使用します。

-   デバイスには、バスに固有の一意の ID が含まれています。

-   デバイスのバス ドライバーは、存在し、正しい形式として、この一意の ID を認識します。

-   バス ドライバーがグローバルに一意の識別子に一意の ID を確実にハッシュことができます (*GUID*) への応答でこの GUID を返します、 [ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)ときに関数コード**Parameters.QueryId.IdType**のメンバー、 [ **IO_STACK_LOCATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)構造に設定されている**BusQueryContainerID**.

Windows 7 および Windows の以降のバージョンは、いくつかの最も一般的なタイプのバスの受信トレイのドライバーを提供します。 これには、USB、Bluetooth、PNP-X 対応が含まれます。 これらのバスの種類のデバイスがのみをバスに固有の一意の ID を含める必要 指定された Windows バス ドライバーは、デバイスから一意の ID を読み取り、コンテナー ID を作成し、

次のトピックでは、受信トレイのバス ドライバーが特定のバスの種類のコンテナーの Id を生成する方法について説明します。

[USB デバイス用のコンテナー Id](container-ids-for-usb-devices.md)

[Bluetooth デバイス用のコンテナー Id](container-ids-for-bluetooth-devices.md)

[PNP-X 対応デバイス用のコンテナー Id](container-ids-for-pnp-x-devices.md)

[1394 デバイス用のコンテナー Id](container-ids-for-1394-devices.md)

[ESATA デバイス用のコンテナー Id](container-ids-for-esata-devices.md)

[PCI Express デバイス用のコンテナー Id](container-ids-for-pci-express-devices.md)

 

 





