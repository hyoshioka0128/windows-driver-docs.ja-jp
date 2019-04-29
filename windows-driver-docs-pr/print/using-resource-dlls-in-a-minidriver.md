---
title: ミニドライバーでリソース DLL を使用する
description: ミニドライバーでリソース DLL を使用する
ms.assetid: b63c48bb-3321-45e0-b37c-a9612a95cc24
keywords:
- GPD は、WDK Unidrv、リソース Dll をファイルします。
- リソース Dll の WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35f74e692a08aa71c20bc6977a874b392a9b5c9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387115"
---
# <a name="using-resource-dlls-in-a-minidriver"></a>ミニドライバーでリソース DLL を使用する





通常、プリンター ドライバーでは、このようなリソースを外部に保存されたフォント、アイコン、およびその他のビットマップ、およびローカライズ可能なユーザー インターフェイスのテキスト文字列としての使用が必要です。 これらの項目の説明は、Microsoft Windows SDK ドキュメント」の説明に従ってリソース DLL に配置されます。

Unidrv ミニドライバーでは、リソース Dll を使用するには、次の方法のいずれかのリソースを識別する必要があります。

-   1 つ以上のリソース DLL を使用している場合は、RESDLL 機能を使用してそれらを特定します。

    RESDLL 機能の使用例は次のとおりです。

    ```cpp
    *Feature: RESDLL
    {
        *Option: FirstRes
        {*Name: "MyFirstRes.dll"}
        *Option: SecondRes
        {*Name: "MySecondRes.dll"}
        *Option: ThirdRes
        {*Name: "MyThirdRes.dll"}
    }
    ```

    これらのリソース Dll のいずれかに含まれるリソースを参照するには、次の形式を使用します。

    RESDLL します。*ResourceOptionName*.*ResourceID*

-   1 つだけのリソース DLL を使用している場合は、値を割り当てることで識別できます、 \*ResourceDLL 属性。

    このリソース DLL に含まれるリソースを参照するには、次の例に示すように、適切なリソース識別子を指定します。

    ```cpp
    *rcNameID: 288
    ```

すべてのリソース、ミニドライバーで使用される Dll は、プリンター INF ファイルで指定する必要があります。 参照してください[Unidrv ミニドライバーをインストールする](installing-a-unidrv-minidriver.md)します。

内で、 *GPD*ファイル、リソースで始まる名前を持つすべてのエントリに値を割り当てる場合、識別子を使用する必要があります\*などの rc \*rcIconID と\*rcCartridgeNameID の例では、します。

さらに、プリンターのハードウェアに常駐フォントの場合は、する必要があります提供[プリンターのフォントの記述](printer-font-descriptions.md).ufm や .ifi のファイルの形式でこれらのフォントは、リソース DLL でこれらのファイルを識別する必要があります、RCを使用して\_UFM または RC\_フォント リソースの種類、それぞれします。

Microsoft 提供の 1 つのリソース DLL の文字列リソースを含む、unires.dll、[標準機能](standard-features.md)と[標準オプション](standard-options.md)します。 Microsoft 提供の GPD ファイル、stdnames.gpd、マクロ シンボル名は、各リソースの識別子を割り当てます。 これにより、マクロ名でこれらのリソースを参照する次の例に示すようにします。

```cpp
*rcNameID: =LETTERSMALL_DISPLAY
```

 

 




