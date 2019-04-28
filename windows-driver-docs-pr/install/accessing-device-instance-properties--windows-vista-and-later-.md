---
title: デバイス インスタンス プロパティへのアクセス
description: デバイス インスタンス プロパティへのアクセス
ms.assetid: b571201a-e765-45d0-993b-5855041b4697
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 863f039cbc12a4e42250658880c292635e4a97c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375716"
---
# <a name="accessing-device-instance-properties"></a>デバイス インスタンス プロパティへのアクセス


アプリケーションとのインストーラーにアクセスできる Windows Vista および以降のバージョンの Windows では、[デバイス インスタンス プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541334)SetupAPI の次の関数を呼び出すことで。

-   [**SetupDiGetDevicePropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551965)

    **SetupDiGetDevicePropertyKeys**関数は、デバイスのインスタンスの現在設定されているデバイスのプロパティを識別するデバイスのプロパティのキーの配列を取得します。 どのようなプロパティがデバイスの設定を決定する方法については、次を参照してください。[決定するプロパティが設定デバイス インスタンス](determining-which-properties-are-set-for-a-device-instance.md)します。

-   [**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

    **SetupDiGetDeviceProperty**関数[デバイス インスタンスに設定されているデバイスのプロパティを取得](retrieving-a-device-instance-property-value.md)します。

-   [**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

    **SetupDiSetDeviceProperty**関数[デバイス インスタンスのデバイス プロパティを設定](setting-a-device-instance-property-value.md)します。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス プロパティにアクセスする方法については、次を参照してください。 [SetupAPI を使用して、デバイス プロパティにアクセスする Configuration Manager](using-setupapi-and-configuration-manager-to-access-device-properties.md)します。

 

 





