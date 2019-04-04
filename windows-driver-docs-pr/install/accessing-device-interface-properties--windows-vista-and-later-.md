---
title: デバイス インターフェイスのプロパティにアクセスします。
description: デバイス インターフェイスのプロパティにアクセスします。
ms.assetid: 8a46816b-56c5-49e9-8250-9ede037ae2b5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c5e127a6c37984645f3edf6e24da09c94a686c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557372"
---
# <a name="accessing-device-interface-properties"></a>デバイス インターフェイスのプロパティにアクセスします。


アプリケーションとのインストーラーにアクセスできる Windows Vista および以降のバージョンの Windows では、[デバイス インターフェイスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541409)SetupAPI の次の関数を呼び出すことで。

-   [**SetupDiGetDeviceInterfacePropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551959)

    **SetupDiGetDeviceInterfacePropertyKeys**関数は、デバイス インターフェイスのインスタンスの現在設定されているデバイスのインターフェイスのプロパティを識別するデバイスのインターフェイス プロパティのキーの配列を取得します。 どのようなプロパティが、デバイス インターフェイスの設定を決定する方法については、[決定するプロパティが設定、デバイス インターフェイス](determining-which-properties-are-set-for-a-device-interface.md)を参照してください。

-   [**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

    **SetupDiGetDeviceInterfaceProperty**関数[デバイス インターフェイスのプロパティを取得](retrieving-a-device-interface-property-value.md)デバイス インターフェイスに設定されています。

-   [**SetupDiSetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552158)

    **SetupDiSetDeviceInterfaceProperty**関数[デバイス インターフェイスのプロパティを設定](setting-a-device-interface-property-value.md)デバイス インターフェイス。

Windows Server 2003、Windows XP、および Windows 2000 でデバイス インターフェイス プロパティにアクセスする方法については、デバイスにアクセスするインターフェイスのプロパティを参照してください。

 

 





