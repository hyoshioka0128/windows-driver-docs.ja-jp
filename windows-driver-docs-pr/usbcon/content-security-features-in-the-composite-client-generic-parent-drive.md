---
Description: Digital Rights Management (DRM) systems often make use of device serial numbers to ensure that legitimate customers have access to digitized intellectual property.
title: Usbccgp.sys のコンテンツのセキュリティ機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 027bba805ecfebe72046357dfab9d2451fa7f51b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559176"
---
# <a name="content-security-features-in-usbccgpsys"></a>Usbccgp.sys のコンテンツのセキュリティ機能


デジタル著作権管理 (DRM) システムが頻繁に活用する正当なユーザーにアクセスできるようにするデバイスのシリアル番号の使用は知的財産権をデジタル化します。 USB デバイスに、CSM 1 コンテンツ セキュリティ インターフェイスがある場合は、クライアント ドライバーを照会できます、シリアル番号を送信して、 [ **IOCTL\_ストレージ\_取得\_メディア\_シリアル\_数**](https://msdn.microsoft.com/library/windows/hardware/ff560557)一般的な親ドライバーに要求します。

## <a name="related-topics"></a>関連トピック
[一般的な親の USB ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



