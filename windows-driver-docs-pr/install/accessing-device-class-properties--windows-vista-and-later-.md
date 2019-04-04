---
title: デバイス クラスのプロパティにアクセスします。
description: デバイス クラスのプロパティにアクセスします。
ms.assetid: 51eef1f4-ca7d-46ab-a33f-be53de277541
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b4d9683e54f8d53c587629e9f3821de976200d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552598"
---
# <a name="accessing-device-class-properties"></a>デバイス クラスのプロパティにアクセスします。


アプリケーションとのインストーラーにアクセスできる Windows Vista および以降のバージョンの Windows では、[デバイス セットアップ クラスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff542239)と[デバイス インターフェイスのクラス プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541406)次 SetupAPI を呼び出すことによって関数:

-   [**SetupDiGetClassPropertyKeys** ](https://msdn.microsoft.com/library/windows/hardware/ff551091)と[ **SetupDiGetClassPropertyKeysEx**](https://msdn.microsoft.com/library/windows/hardware/ff551093)

    **SetupDiGetClassPropertyKeys**関数は、ローカル コンピューター上のデバイス セットアップ クラスまたはデバイスのインターフェイス クラスを現在設定されているクラスのプロパティを識別するクラスのプロパティのキーの配列を取得します。 **SetupDiGetClassPropertyKeysEx**関数がローカル コンピューターまたはリモート コンピューターで同じ操作を実行します。 デバイス クラスのどのようなプロパティが設定を確認する方法については、[を決定するプロパティ設定のデバイス クラスに対する](determining-which-properties-are-set-for-a-device-class.md)を参照してください。

-   [**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

    **SetupDiGetClassProperty**関数[クラス プロパティを取得](retrieving-a-device-class-property-value.md)デバイス セットアップ クラスまたはデバイスのインターフェイス クラス。 [ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)関数は、リモート コンピューター上とローカル コンピューターで同じ操作を実行します。

-   [**SetupDiSetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552128)

    **SetupDiSetClassProperty**関数[デバイス セットアップ クラスまたはデバイスのインターフェイス クラスのクラス プロパティを設定](setting-a-device-class-property-value.md)します。 [ **SetupDiSetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552132)関数は、リモート コンピューター上とローカル コンピューターで同じ操作を実行します。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス クラス プロパティにアクセスする方法については、次を参照してください[へのアクセスのデバイス セットアップ クラスのプロパティ](accessing-device-setup-class-properties.md)と[プロパティへのアクセス デバイス インターフェイス クラス。](accessing-device-interface-class-properties.md)

 

 





