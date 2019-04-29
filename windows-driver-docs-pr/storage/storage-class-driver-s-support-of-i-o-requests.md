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
ms.openlocfilehash: a023df0bec38f35033bf5fc7250d767f878d51ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329613"
---
# <a name="storage-class-drivers-support-of-io-requests"></a>記憶域クラス ドライバーの I/O 要求サポート


## <span id="ddk_storage_class_drivers_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SUPPORT_OF_I_O_REQUESTS_KG"></span>


クラスのまったく新しい種類のストレージ デバイス ドライバーのデザイナーには、デバイスの性質によって、サポートするために、ドライバーの I/O 要求の適切なセットを判断する必要があります。 一般にサポートされる要求のセットは、次の少なくとも。

[**IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff550729)と、デバイスの種類によって、または対称[ **IRP\_MJ\_閉じる**](https://msdn.microsoft.com/library/windows/hardware/ff550720)

[**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550744)

[**IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)、 [ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)、またはその両方

[**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)

[**IRP\_MJ\_電源**](https://msdn.microsoft.com/library/windows/hardware/ff550784)

[**IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813)

 

 




