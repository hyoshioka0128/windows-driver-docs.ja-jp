---
title: GPD または PPD ファイルに基づいて構成モジュール
description: GPD または PPD ファイルに基づいて構成モジュール
ms.assetid: b0aeea58-1c58-475e-8d4a-597778e42a7c
keywords:
- バージョン 3 XPS ドライバー WDK XPSDrv、GPD ファイル
- バージョン 3 XPS ドライバー WDK XPSDrv、PPD ファイル
- GPD ファイル WDK XPSDrv
- PPD ファイル WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cd79dada49ce41896df9ddb766fd63a10b6e478
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528069"
---
# <a name="configuration-modules-based-on-gpd-or-ppd-files"></a>GPD または PPD ファイルに基づいて構成モジュール


Windows vista の場合、GPD と PPD ファイルには、印刷スキーマのマッピングが含まれています、XPSDrv に固有の新しいエントリは印刷ドライバー。 これらの変更は、Unidrv または Pscript5 構成モジュールは印刷ドライバー プラグインを GPD 専用または PPD 専用の構成モジュールを作成する際に、GPD と PPD ファイルに適用されます。

### <a name="xpsdrv-specific-gpd-and-ppd-entries"></a>XPSDrv 固有 GPD と PPD エントリ

GPD または PPD ファイルを使用して、XPSDrv プリンター ドライバーのバージョン 3 の印刷ドライバー構成モジュールを作成するには、次のいずれかを行う必要があります。

-   作成または GPD または PPD ファイルを編集します。 ファイルには、プリンターがサポートする機能を説明する構成キーワードを含める必要があります。 標準 GPD または PPD キーワードは、パブリックの印刷スキーマ キーワードを自動的にマップされますが、非標準のキーワードは、既定では、プライベートの名前空間にマップされます。

-   PPD ファイルを作成する場合、GPD ファイル、または、Msxpsinc.ppd ファイルを作成している場合は、Msxpsinc.gpd ファイルが含まれます。 これらのファイルには、結果の構成ファイルが XPSDrv プリンターのドライバーの一部をすることを示す、次のキーワードが含まれます。

    Msxpsinc.gpd に含まれています。

    ```cpp
    IsXPSDriver?: TRUE
    ```

    Msxpsinc.ppd に含まれています。

    ```cpp
    *MSIsXPSDriver: True
    ```

これらの属性、GPD または PPD ファイルに追加するのではなく、優先のアプローチには、Msxpsinc.gpd Msxpsinc.ppd ファイルなどです。 Microsoft では、適切なインクルード ファイルに XPSDrv ドライバーの将来の属性を追加できます。 Microsoft では、インクルード ファイルに新しい属性を追加し、GPD または PPD ファイルにインクルード ファイルを使用して場合、は、印刷ドライバーの GPD または PPD ファイルを編集する必要はありません。

ルート GPD または PPD ファイル (ドライバーの INF ファイルで指定される`DataFile`) のすべての Microsoft Unidrv または PScript5 のドライバーに基づいた XPSDrv ドライバーが、対応する Msxpsinc.gpd または Msxpsinc.ppd ファイルを含める必要があります。

たとえば、モデル-foo.gpd のとおりです。

```cpp
*Include: "msxpsinc.gpd"
```

モデル-foo.ppd が含まれます。

```cpp
*Include: "msxpinc.ppd"
```

### <a name="print-schema-mapping"></a>印刷スキーマ マッピング

印刷スキーマのマッピングは、パブリック、相当する印刷スキーマ キーワード GPD と PPD キーワードを変換する Unidrv PScript5 構成モジュールの機能です。 既定では、すべての標準的な GPD と PPD キーワードは、同等のパブリック印刷スキーマ キーワードにマップされます。 GPD または PPD ファイルでは、非標準のキーワードただし、プライベートのデバイスに固有の名前空間に既定でマッピングされます。 次のいずれかの手順を実行して、このマッピングを改善できます。

-   非標準のキーワードの秘密の名前空間を指定します。

-   GPD または PPD ファイル内のパブリックの印刷スキーマから同等のキーワードと GPD または PPD ファイルの機能とオプションのキーワードを非標準の関連付け。 この関連付けは、印刷スキーマの公開機能として PrintTicket と PrintCapabilities データを生成するには構成モジュールを使用できます。

### <a name="gpd-file-example"></a>GPD ファイルの例

次のコード例は、エントリを示す GPD ファイルを示し、XPSDrv、バージョン 3 の構成モジュールを作成するためのキーワードは印刷ドライバー。

```cpp
*%
*% Copyright (c) 2004 - 2006 Microsoft Corporation
*% All Rights Reserved.
*%
*GPDFileVersion: "1.0"
*GPDSpecVersion: "1.0"
*GPDFileName:    "plugfest.gpd"
*Include:        "StdNames.gpd"
*%
*% Include XPSDrv include file
*%
*Include:        "MSXpsInc.gpd"
*ModelName:      "Microsoft XPS Passthrough Driver Sample"
*MasterUnits:    PAIR(1200, 1200)
*ResourceDLL:    "unires.dll"
*PrinterType:    PAGE
*MaxCopies:      1

*%
*% IHV Private Namespace
*%
*PrintSchemaPrivateNamespaceURI:"http://www.ihv.com/schema/2006"
*%
*% IHV Private Feature
*%
*Feature: IHVStapling { 
*PrintSchemaKeywordMap: "JobStapleAllDocuments"
*Option: Enabled {
  *PrintSchemaKeywordMap: "StapleTopLeft" }
*Option: Disabled {
  *PrintSchemaKeywordMap: "None"  }
}
```

 

 




