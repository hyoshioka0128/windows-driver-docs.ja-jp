---
title: デバイス インスタンス プロパティへのアクセス
description: デバイス インスタンス プロパティへのアクセス
ms.assetid: b571201a-e765-45d0-993b-5855041b4697
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a03fe0ddebf2ec762a05cfd7b2fef63ba4dc745
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359240"
---
# <a name="accessing-device-instance-properties"></a>デバイス インスタンス プロパティへのアクセス


アプリケーションとのインストーラーにアクセスできる Windows Vista および以降のバージョンの Windows では、[デバイス インスタンス プロパティ](https://docs.microsoft.com/previous-versions/ff541334(v=vs.85))SetupAPI の次の関数を呼び出すことで。

-   [**SetupDiGetDevicePropertyKeys**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)

    **SetupDiGetDevicePropertyKeys**関数は、デバイスのインスタンスの現在設定されているデバイスのプロパティを識別するデバイスのプロパティのキーの配列を取得します。 どのようなプロパティがデバイスの設定を決定する方法については、次を参照してください。[決定するプロパティが設定デバイス インスタンス](determining-which-properties-are-set-for-a-device-instance.md)します。

-   [**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

    **SetupDiGetDeviceProperty**関数[デバイス インスタンスに設定されているデバイスのプロパティを取得](retrieving-a-device-instance-property-value.md)します。

-   [**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

    **SetupDiSetDeviceProperty**関数[デバイス インスタンスのデバイス プロパティを設定](setting-a-device-instance-property-value.md)します。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス プロパティにアクセスする方法については、次を参照してください。 [SetupAPI を使用して、デバイス プロパティにアクセスする Configuration Manager](using-setupapi-and-configuration-manager-to-access-device-properties.md)します。

 

 





