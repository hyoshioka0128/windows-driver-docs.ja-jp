---
title: デバイス インターフェイス プロパティへのアクセス
description: デバイス インターフェイス プロパティへのアクセス
ms.assetid: 8a46816b-56c5-49e9-8250-9ede037ae2b5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c5e127a6c37984645f3edf6e24da09c94a686c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361188"
---
# <a name="accessing-device-interface-properties"></a>デバイス インターフェイス プロパティへのアクセス


アプリケーションとのインストーラーにアクセスできる Windows Vista および以降のバージョンの Windows では、[デバイス インターフェイスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541409)SetupAPI の次の関数を呼び出すことで。

-   [**SetupDiGetDeviceInterfacePropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551959)

    **SetupDiGetDeviceInterfacePropertyKeys**関数は、デバイス インターフェイスのインスタンスの現在設定されているデバイスのインターフェイスのプロパティを識別するデバイスのインターフェイス プロパティのキーの配列を取得します。 どのようなプロパティが、デバイス インターフェイスの設定を決定する方法については、次を参照してください。[決定するプロパティが設定、デバイス インターフェイス](determining-which-properties-are-set-for-a-device-interface.md)します。

-   [**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

    **SetupDiGetDeviceInterfaceProperty**関数[デバイス インターフェイスのプロパティを取得](retrieving-a-device-interface-property-value.md)デバイス インターフェイスに設定されています。

-   [**SetupDiSetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552158)

    **SetupDiSetDeviceInterfaceProperty**関数[デバイス インターフェイスのプロパティを設定](setting-a-device-interface-property-value.md)デバイス インターフェイス。

Windows Server 2003、Windows XP、および Windows 2000 でデバイス インターフェイス プロパティにアクセスする方法については、デバイスにアクセスするインターフェイスのプロパティを参照してください。

 

 





