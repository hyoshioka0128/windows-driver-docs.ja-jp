---
title: デバイス インスタンスのプロパティにアクセスします。
description: デバイス インスタンスのプロパティにアクセスします。
ms.assetid: b571201a-e765-45d0-993b-5855041b4697
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 863f039cbc12a4e42250658880c292635e4a97c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538818"
---
# <a name="accessing-device-instance-properties"></a>デバイス インスタンスのプロパティにアクセスします。


アプリケーションとのインストーラーにアクセスできる Windows Vista および以降のバージョンの Windows では、[デバイス インスタンス プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541334)SetupAPI の次の関数を呼び出すことで。

-   [**SetupDiGetDevicePropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551965)

    **SetupDiGetDevicePropertyKeys**関数は、デバイスのインスタンスの現在設定されているデバイスのプロパティを識別するデバイスのプロパティのキーの配列を取得します。 どのようなプロパティがデバイスの設定を決定する方法については、[決定するプロパティが設定デバイス インスタンス](determining-which-properties-are-set-for-a-device-instance.md)を参照してください。

-   [**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

    **SetupDiGetDeviceProperty**関数[デバイス インスタンスに設定されているデバイスのプロパティを取得](retrieving-a-device-instance-property-value.md)します。

-   [**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

    **SetupDiSetDeviceProperty**関数[デバイス インスタンスのデバイス プロパティを設定](setting-a-device-instance-property-value.md)します。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス プロパティにアクセスする方法については、[SetupAPI を使用して、デバイス プロパティにアクセスする Configuration Manager](using-setupapi-and-configuration-manager-to-access-device-properties.md)を参照してください。

 

 





