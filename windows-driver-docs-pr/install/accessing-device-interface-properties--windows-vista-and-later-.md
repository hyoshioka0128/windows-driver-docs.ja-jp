---
title: デバイス インターフェイス プロパティへのアクセス
description: デバイス インターフェイス プロパティへのアクセス
ms.assetid: 8a46816b-56c5-49e9-8250-9ede037ae2b5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92fc771822fd6e7b258d1c72596a98c4f5db5d28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383033"
---
# <a name="accessing-device-interface-properties"></a>デバイス インターフェイス プロパティへのアクセス


アプリケーションとのインストーラーにアクセスできる Windows Vista および以降のバージョンの Windows では、[デバイス インターフェイスのプロパティ](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))SetupAPI の次の関数を呼び出すことで。

-   [**SetupDiGetDeviceInterfacePropertyKeys**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys)

    **SetupDiGetDeviceInterfacePropertyKeys**関数は、デバイス インターフェイスのインスタンスの現在設定されているデバイスのインターフェイスのプロパティを識別するデバイスのインターフェイス プロパティのキーの配列を取得します。 どのようなプロパティが、デバイス インターフェイスの設定を決定する方法については、次を参照してください。[決定するプロパティが設定、デバイス インターフェイス](determining-which-properties-are-set-for-a-device-interface.md)します。

-   [**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

    **SetupDiGetDeviceInterfaceProperty**関数[デバイス インターフェイスのプロパティを取得](retrieving-a-device-interface-property-value.md)デバイス インターフェイスに設定されています。

-   [**SetupDiSetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

    **SetupDiSetDeviceInterfaceProperty**関数[デバイス インターフェイスのプロパティを設定](setting-a-device-interface-property-value.md)デバイス インターフェイス。

Windows Server 2003、Windows XP、および Windows 2000 でデバイス インターフェイス プロパティにアクセスする方法については、デバイスにアクセスするインターフェイスのプロパティを参照してください。

 

 





