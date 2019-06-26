---
title: 記憶域クラス ドライバーの I/O 要求サポート
description: 記憶域クラス ドライバーの I/O 要求サポート
ms.assetid: 046b7978-49ee-4e3e-a85f-f6ad327b91bf
keywords:
- 記憶域クラス ドライバー WDK、I/O 要求のサポート
- クラス ドライバー WDK の記憶域、I/O 要求のサポート
- I/O 要求の WDK ストレージ
- Irp WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba778556d13fcac51beedfc64d1098f33b80a1d5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368867"
---
# <a name="storage-class-drivers-support-of-io-requests"></a>記憶域クラス ドライバーの I/O 要求サポート


## <span id="ddk_storage_class_drivers_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SUPPORT_OF_I_O_REQUESTS_KG"></span>


クラスのまったく新しい種類のストレージ デバイス ドライバーのデザイナーには、デバイスの性質によって、サポートするために、ドライバーの I/O 要求の適切なセットを判断する必要があります。 一般にサポートされる要求のセットは、次の少なくとも。

[**IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)と、デバイスの種類によって、または対称[ **IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[**IRP\_MJ\_DEVICE\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)

[**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)、 [ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)、またはその両方

[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

[**IRP\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)

[**IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)

 

 




