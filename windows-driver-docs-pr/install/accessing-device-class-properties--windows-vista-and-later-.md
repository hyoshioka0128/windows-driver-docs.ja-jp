---
title: デバイス クラス プロパティへのアクセス
description: デバイス クラス プロパティへのアクセス
ms.assetid: 51eef1f4-ca7d-46ab-a33f-be53de277541
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e583302d1feebb5f57d8d5ba26b80425a92a21b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385634"
---
# <a name="accessing-device-class-properties"></a>デバイス クラス プロパティへのアクセス


アプリケーションとのインストーラーにアクセスできる Windows Vista および以降のバージョンの Windows では、[デバイス セットアップ クラスのプロパティ](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))と[デバイス インターフェイスのクラス プロパティ](https://docs.microsoft.com/previous-versions/ff541406(v=vs.85))次 SetupAPI を呼び出すことによって関数:

-   [**SetupDiGetClassPropertyKeys** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys)と[ **SetupDiGetClassPropertyKeysEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw)

    **SetupDiGetClassPropertyKeys**関数は、ローカル コンピューター上のデバイス セットアップ クラスまたはデバイスのインターフェイス クラスを現在設定されているクラスのプロパティを識別するクラスのプロパティのキーの配列を取得します。 **SetupDiGetClassPropertyKeysEx**関数がローカル コンピューターまたはリモート コンピューターで同じ操作を実行します。 デバイス クラスのどのようなプロパティが設定を確認する方法については、次を参照してください。[を決定するプロパティ設定のデバイス クラスに対する](determining-which-properties-are-set-for-a-device-class.md)します。

-   [**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

    **SetupDiGetClassProperty**関数[クラス プロパティを取得](retrieving-a-device-class-property-value.md)デバイス セットアップ クラスまたはデバイスのインターフェイス クラス。 [ **SetupDiGetClassPropertyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)関数は、リモート コンピューター上とローカル コンピューターで同じ操作を実行します。

-   [**SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

    **SetupDiSetClassProperty**関数[デバイス セットアップ クラスまたはデバイスのインターフェイス クラスのクラス プロパティを設定](setting-a-device-class-property-value.md)します。 [ **SetupDiSetClassPropertyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)関数は、リモート コンピューター上とローカル コンピューターで同じ操作を実行します。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス クラス プロパティにアクセスする方法については、次を参照してください[へのアクセスのデバイス セットアップ クラスのプロパティ](accessing-device-setup-class-properties.md)と[プロパティへのアクセス デバイス インターフェイス クラス。](accessing-device-interface-class-properties.md)

 

 





