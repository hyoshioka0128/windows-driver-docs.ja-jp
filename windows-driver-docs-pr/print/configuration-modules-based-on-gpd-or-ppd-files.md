---
title: GPD または PPD ファイルを基盤とする構成モジュール
description: GPD または PPD ファイルを基盤とする構成モジュール
ms.assetid: b0aeea58-1c58-475e-8d4a-597778e42a7c
keywords:
- バージョン 3 XPS ドライバー WDK XPSDrv、GPD files
- バージョン 3 XPS ドライバー WDK XPSDrv、PPD ファイル
- GPD ファイル WDK XPSDrv
- PPD ファイル WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7bc56ecf70727b06d8c17e3f556fbe8496a4eb4
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652853"
---
# <a name="configuration-modules-based-on-gpd-or-ppd-files"></a>GPD または PPD ファイルを基盤とする構成モジュール


Windows Vista の場合、GPD ファイルと PPD ファイルには、印刷スキーママッピングと XPSDrv 印刷ドライバーに固有の新しいエントリが含まれています。 これらの変更は GPD および PPD ファイルに適用されます。これらのファイルを使用すると、Unidrv または Pscript5 print driver プラグイン用の GPD または PPD 専用の構成モジュールと構成モジュールを作成できます。

### <a name="xpsdrv-specific-gpd-and-ppd-entries"></a>XPSDrv 固有の GPD と PPD エントリ

GPD または PPD ファイルを使用して XPSDrv print driver 用のバージョン3の印刷ドライバー構成モジュールを作成するには、次のいずれかの操作を行う必要があります。

-   GPD ファイルまたは PPD ファイルを作成または編集します。 このファイルには、プリンターでサポートされている機能を説明する構成キーワードを含める必要があります。 標準の GPD または PPD キーワードは、public Print Schema キーワードに自動的にマップされますが、非標準のキーワードは既定でプライベート名前空間にマップされます。

-   GPD ファイルを作成している場合は msgpd ファイルを、PPD ファイルを作成する場合は Ms ファイルを含めます (たとえば、)。 これらのファイルには、次のキーワードが含まれます。これは、結果として得られる構成ファイルが XPSDrv print ドライバーの一部であることを示します。

    Gpd の場合、次のものが含まれます。

    ```cpp
    IsXPSDriver?: TRUE
    ```

    Msxp の場合は、次のものが含まれます。

    ```cpp
    *MSIsXPSDriver: True
    ```

これらの属性を GPD または PPD ファイルに追加するのではなく、Msxp singpd または Msxp をインクルードする方法をお勧めします。 Microsoft では、XPSDrv ドライバーの将来の属性を適切なインクルードファイルに追加できます。 Microsoft が新しい属性をインクルードファイルに追加し、GPD ファイルまたは PPD ファイルでインクルードファイルを使用する場合は、印刷ドライバーの GPD または PPD ファイルを編集する必要はありません。

Microsoft Unidrv または PScript5 ドライバーベースのすべての XPSDrv ドライバーのルート GPD ファイルまたは PPD ファイル (ドライバーの `DataFile`として指定されています) には、対応する msGPD またはファイルが含まれている必要があります。

たとえば、Model-foo の場合は、次のように指定します。

```cpp
*Include: "msxpsinc.gpd"
```

Model-foo の場合は、次のものを含めます。

```cpp
*Include: "msxpinc.ppd"
```

### <a name="print-schema-mapping"></a>印刷スキーママッピング

印刷スキーママッピングは、GPD および PPD キーワードを同等の公開印刷スキーマキーワードに変換する、Unidrv および PScript5 構成モジュールの機能です。 既定では、すべての standard GPD と PPD キーワードは、同等の公開印刷スキーマキーワードにマップされます。 ただし、GPD ファイルまたは PPD ファイル内の非標準のキーワードは、既定では、プライベートのデバイス固有の名前空間にマップされます。 このマッピングを改善するには、次のいずれかまたは両方を実行します。

-   非標準のキーワードにプライベート名前空間を指定します。

-   GPD または PPD ファイル内の非標準の機能キーワードとオプションキーワードを、GPD または PPD ファイル内の公開された印刷スキーマと同等のキーワードに関連付けます。 この関連付けにより、構成モジュールは、パブリックな印刷スキーマ機能として、PrintTicket および PrintCapabilities データを生成できます。

### <a name="gpd-file-example"></a>GPD ファイルの例

次のコード例は、XPSDrv 印刷ドライバーのバージョン3構成モジュールを作成するためのエントリとキーワードを示す GPD ファイルを示しています。

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
*PrintSchemaPrivateNamespaceURI:"https://www.ihv.com/schema/2006"
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

 

 




