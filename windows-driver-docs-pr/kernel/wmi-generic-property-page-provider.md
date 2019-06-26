---
title: WMI の汎用プロパティ ページ プロバイダー
description: WMI の汎用プロパティ ページ プロバイダー
ms.assetid: 44cfafdf-c8e2-4175-95e5-3c5d03dc206d
keywords:
- WMI の WDK カーネルでは、プロパティ シート
- プロパティ シートの WDK WMI
- 汎用プロパティ ページ プロバイダー WDK WMI
- プロパティ ページの WDK WMI
- プロパティ修飾子 WDK WMI
- デバイスのプロパティ シートの WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd7de792ebbbae30f6327763944a09655d2e0698
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386998"
---
# <a name="wmi-generic-property-page-provider"></a>WMI の汎用プロパティ ページ プロバイダー





Windows XP およびそれ以降のオペレーティング システム、ドライバーは、WMI の汎用プロパティ ページのプロバイダーでは、その WMI クラスを公開できます。 プロバイダーでは、各クラスの宣言を使用して、クラスのプロパティの単純なプロパティ ページを作成します。

### <a name="how-property-qualifiers-determine-the-property-page"></a>プロパティの修飾子が、プロパティ ページを確認する方法

WMI 汎用プロパティのページ プロバイダーでは、クラスの各プロパティのデータ型の適切なコントロールを使用します。 次のプロパティの修飾子は、使用されるコントロールの種類を変更します。

-   **書き込み**

    プロパティを**書き込み**プロパティ ページで、修飾子を変更できます。 それ以外の場合、プロパティは読み取り専用です。

-   **値**と**ValuesMap**

    汎用プロパティ ページのプロバイダーでは、リスト ボックスを使用して、使用可能な値を表します。

-   **範囲**

    汎用プロパティ ページのプロバイダーは、入力されたデータが指定された範囲に準拠していることを検証します。

-   **DisplayName**

    汎用プロパティ ページのプロバイダーは、プロパティのラベルとしてプロパティ修飾子の値を使用します。

-   **DisplayInHex**

    存在する場合、プロパティの値が 16 進数で表示されます。

ドライバー開発者は、文字列のプロパティの修飾子をローカライズする必要があります。 参照してください[MOF ファイルのローカライズ](localizing-mof-files.md)詳細についてはします。

### <a name="enabling-the-generic-property-page-provider"></a>汎用プロパティ ページのプロバイダーを有効にします。

Wmiprop.dll で使用されるクラスを公開する各デバイスでは、共同インストーラーとして Wmiprop.dll を有効にする必要があります。 これを行うには、次の追加を行う共同インストーラーに*追加レジストリ セクション*: クラス GUID の値のエントリを追加で、 **HKLM\\システム\\CurrentControlSet\\コントロール\\CoDeviceInstallers**レジストリ キー。 値のエントリの値は、"WmiProp.dll WmiPropCoInstaller"です。

例:

```cpp
; This section is defined in the Co-installer section, as follows.
; [Co-installer]
; AddReg = CoInstaller_AddReg

[CoInstaller_AddReg] 
HKLM, System\CurrentControlSet\Control\CoDeviceInstallers, ClassGUID,
    0x00010000, "WmiProp.dll, WmiPropCoInstaller"
```

*ClassGUID*は WMI クラスの GUID です。 参照してください[クラス共同インストーラーを登録する](https://docs.microsoft.com/windows-hardware/drivers/install/registering-a-class-co-installer)詳細についてはします。

汎用プロパティ プロバイダーを介して公開する特定の WMI クラスを指定することも必要があります。 これを行うには、次のように設定します。、 **WmiConfigClasses**クラス、WMI のコンマ区切りの一覧を示す値、*追加レジストリ セクション*のデバイス クラスまたはデバイスのハードウェアのインスタンス。

```cpp
; the device class AddReg section.
[device_class_AddReg]
HKR,,"WmiConfigClasses",0x00000000,"class1,class2"

; the device hardware instance AddReg section.
[device_hw_inst_AddReg]
HKR,,"WmiConfigClasses",0x00000000,"class3"
```

参照してください[ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)の説明については、*追加レジストリ セクション*INF ファイルでします。

Wmiprop.dll は、各クラスのインスタンスを 1 つだけを想定しています。 各クラスは、プロパティ シートのタブで表されます。 使用して、 **DisplayName**プロパティ修飾子 タブのタイトル テキストを設定します。クラスのプロパティ ページは、現在、クラスのインスタンスがある場合にのみ表示されます。 そのため、デバイスが削除または開始されていない場合、ページは表示されません。

 

 




