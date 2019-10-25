---
Description: 多くの場合、デジタル Rights Management (DRM) システムはデバイスのシリアル番号を使用して、正当な顧客がデジタル化された知的財産権を持つことができるようにします。
title: Usbccgp.sys のコンテンツ セキュリティ機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59d7faabb4ab369405b1d67f80cf2223f0208086
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842398"
---
# <a name="content-security-features-in-usbccgpsys"></a>Usbccgp.sys のコンテンツ セキュリティ機能


多くの場合、デジタル Rights Management (DRM) システムはデバイスのシリアル番号を使用して、正当な顧客がデジタル化された知的財産権を持つことができるようにします。 USB デバイスに CSM-1 コンテンツセキュリティインターフェイスが含まれている場合、クライアントドライバーは、IOCTL\_ストレージ\_送信してシリアル番号を照会し、 [ **\_メディア\_シリアル\_番号**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number)要求を汎用の親ドライバーに取得します。

## <a name="related-topics"></a>関連トピック
[USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



