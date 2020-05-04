---
title: デバイス プロパティを変更する INF ファイルのエントリ値
description: デバイス プロパティを変更する INF ファイルのエントリ値
ms.assetid: 5ce0875f-2687-42d9-b980-ed184b552a62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e559695ecaa71a3924d620c5f05600527571eb
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223160"
---
# <a name="inf-file-entry-values-that-modify-device-properties"></a>デバイス プロパティを変更する INF ファイルのエントリ値


Windows Vista 以降のデバイスのプロパティを変更する INF ファイルのエントリ値を次に示します。

-   対応する[システム定義のデバイスプロパティ](system-defined-device-properties2.md)を設定する INF ファイルエントリ値。

-   [**Inf AddReg ディレクティブ**](inf-addreg-directive.md)および[**inf delreg ディレクティブ**](inf-delreg-directive.md)。システム定義のデバイスプロパティに対応するシステム定義のレジストリエントリ値を設定または削除します。

-   カスタムレジストリエントリ値を設定または削除する INF **AddReg**ディレクティブおよび Inf **delreg**ディレクティブ

-   [**Inf AddProperty ディレクティブ**](inf-addproperty-directive.md)および**inf delproperty ディレクティブ**。デバイスのプロパティを設定および削除します。 これらのディレクティブの使用方法の詳細については、「 [Inf AddProperty ディレクティブと Inf DelProperty ディレクティブの使用](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)」を参照してください。

デバイスインスタンス、[デバイスセットアップクラス](device-setup-classes.md)、[デバイスインターフェイスクラス](device-interface-classes.md)、デバイスインターフェイスをインストールする INF ファイルのセクションに関する一般的な情報については、次のトピックを参照してください。

[**INF *Ddinstall*セクション**](inf-ddinstall-section.md)

[**INF ClassInstall32 セクション**](inf-classinstall32-section.md)

[**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)

[**INF *Ddinstall*。インターフェイスセクション**](inf-ddinstall-interfaces-section.md)

### <a name="inf-file-entry-values-that-set-corresponding-system-defined-device-properties"></a><a href="" id="inf-file-entry-values-that-set-corresponding-system-defined-device-pro"></a>対応するシステム定義のデバイスプロパティを設定する INF ファイルエントリ値

一部の INF ファイルエントリ値は、対応するシステム定義のデバイスプロパティを設定するために Windows で使用される情報を提供します。 次に、このような INF ファイルエントリ値によって値が提供されるデバイスプロパティの例をいくつか示します。

-   デバイスインスタンスの[**DEVPKEY_Device_DeviceDesc**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-devicedesc)プロパティは、[ [**INF モデル] セクション**](inf-models-section.md)の [*デバイス-説明*] エントリ値によって設定されます。

-   [デバイスセットアップクラス](device-setup-classes.md)の[**DEVPKEY_DeviceClass_ClassName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-classname)プロパティは、 [**Inf バージョンセクション**](inf-version-section.md)の inf**クラス**ディレクティブの*クラス名*エントリ値によって設定されます。

-   デバイスインターフェイスの[**DEVPKEY_DeviceInterface_ClassGuid**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceinterface-classguid)プロパティは、 [**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)の*InterfaceClassGuid*エントリ値によって設定されます。

### <a name="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-defined-device-properties"></a><a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-def"></a>INF AddReg ディレクティブと INF DelReg ディレクティブ (システム定義のデバイスプロパティを変更する)

システム定義のデバイスプロパティの多くには、対応するシステム定義のレジストリエントリ値があります。 対応するレジストリエントリ値を持つデバイスプロパティの場合、 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)を使用して対応するレジストリエントリ値を追加すると、対応するデバイスプロパティが設定されます。 同様に、 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)を使用してレジストリエントリ値を削除すると、対応するデバイスプロパティが削除されます。

たとえば、次の**AddReg**ディレクティブは、"ABC_DEVICE_INSTALL. HW" セクションによってインストールされたデバイスインスタンスの**DeviceCharacteristics**レジストリエントリ値と対応する DEVPKEY_Device_Characteristics プロパティを設定します。

```inf
[Abc_Device_Install.HW]
...
AddReg = Xxx_AddReg
...
[Xxx_AddReg]
...
[HKR,,DeviceCharacteristics,0x10001,0x00000001
] 
```

### <a name="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-registry-entry-values"></a><a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-reg"></a>カスタムレジストリエントリ値を変更する INF AddReg ディレクティブおよび INF DelReg ディレクティブ

Windows Vista 以降のバージョンでは、 [**Inf AddReg ディレクティブ**](inf-addreg-directive.md)と[**inf delreg ディレクティブ**](inf-delreg-directive.md)を使用して、カスタムデバイスプロパティを表すカスタムレジストリエントリ値を変更できます。 ただし、デバイスのプロパティを表すカスタムレジストリエントリの値を作成することは、統合されたデバイスのプロパティモデルではサポートされていません。 デバイスのカスタムレジストリエントリの値を作成する場合は、Windows Server 2003、Windows XP、および Windows 2000 で管理する場合と同じ方法でレジストリエントリの値を管理する必要があります。 カスタムのデバイスプロパティの管理を簡略化するには、カスタムレジストリエントリ値を作成するのではなく、カスタムデバイスプロパティを表すデバイスプロパティキーを作成する必要があります。









