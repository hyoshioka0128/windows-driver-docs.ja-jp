---
Description: デジタル著作権管理 (DRM) システムが頻繁に活用する正当なユーザーにアクセスできるようにするデバイスのシリアル番号の使用は知的財産権をデジタル化します。
title: Usbccgp.sys のコンテンツ セキュリティ機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2784727d29e18fb93c15103a63f3a12097a93cd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378351"
---
# <a name="content-security-features-in-usbccgpsys"></a>Usbccgp.sys のコンテンツ セキュリティ機能


デジタル著作権管理 (DRM) システムが頻繁に活用する正当なユーザーにアクセスできるようにするデバイスのシリアル番号の使用は知的財産権をデジタル化します。 USB デバイスに、CSM 1 コンテンツ セキュリティ インターフェイスがある場合は、クライアント ドライバーを照会できます、シリアル番号を送信して、 [ **IOCTL\_ストレージ\_取得\_メディア\_シリアル\_数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number)一般的な親ドライバーに要求します。

## <a name="related-topics"></a>関連トピック
[一般的な親の USB ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



