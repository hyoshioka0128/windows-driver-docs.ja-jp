---
title: デバイス プロパティを変更する INF ファイルのエントリ値
description: デバイス プロパティを変更する INF ファイルのエントリ値
ms.assetid: 5ce0875f-2687-42d9-b980-ed184b552a62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4412180ff2ee00ed20e73490e409867b9eb15730
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574026"
---
# <a name="inf-file-entry-values-that-modify-device-properties"></a>デバイス プロパティを変更する INF ファイルのエントリ値


以下は、Windows Vista 以降のデバイス プロパティを変更する INF ファイル エントリの値です。

-   そのセットの対応する INF ファイルのエントリの値[デバイスのシステム定義プロパティ](system-defined-device-properties2.md)します。

-   [**INF AddReg ディレクティブ**](inf-addreg-directive.md)と[ **INF してディレクティブ**](inf-delreg-directive.md)を設定またはデバイスのシステム定義のプロパティに対応するシステム定義のレジストリ エントリの値を削除します。

-   INF **AddReg**ディレクティブと INF**して**ディレクティブを設定またはカスタムのレジストリ エントリの値を削除します。

-   [**INF AddProperty ディレクティブ**](inf-addproperty-directive.md)と**INF DelProperty ディレクティブ**設定して、デバイスのプロパティを削除します。 これらのディレクティブを使用する方法の詳細については、[INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)を参照してください。

概要については、INF ファイルのセクションでは、デバイスのインスタンスをインストールする[デバイス セットアップ クラス](device-setup-classes.md)、[デバイス インターフェイス クラス](device-interface-classes.md)、し、デバイスのインターフェイスは、次のトピックを参照してください。

[**INF *DDInstall*セクション**](inf-ddinstall-section.md)

[**INF ClassInstall32 セクション**](inf-classinstall32-section.md)

[**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)

[**INF *DDInstall*します。インターフェイス セクション**](inf-ddinstall-interfaces-section.md)

### <a href="" id="inf-file-entry-values-that-set-corresponding-system-defined-device-pro"></a>INF ファイルのエントリの対応するデバイスのシステム定義のプロパティが設定される値します。

いくつかの INF ファイル エントリの値は、Windows が対応するデバイスのシステム定義のプロパティの設定に使用する情報を提供します。 デバイスのプロパティの値は、このような INF ファイル エントリの値によって提供されますのいくつかの例を次に示します。

-   [ **DEVPKEY_Device_DeviceDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff542407)デバイス インスタンスのプロパティが設定されて、*デバイス説明*エントリの値で、 [ **INFセクションをモデル化**](inf-models-section.md)します。

-   [ **DEVPKEY_DeviceClass_ClassName** ](https://msdn.microsoft.com/library/windows/hardware/ff542272)プロパティを[デバイス セットアップ クラス](device-setup-classes.md)で設定されて、*クラス名*INFでエントリの値**クラス**ディレクティブで、 [ **INF バージョン セクション**](inf-version-section.md)します。

-   [ **DEVPKEY_DeviceInterface_ClassGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff542349)デバイス インターフェイスのプロパティが設定されて、 *InterfaceClassGuid*エントリの値で、 [ **INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)します。

### <a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-def"></a>INF AddReg ディレクティブとデバイスのシステム定義のプロパティを変更する INF してディレクティブ

多くのシステム定義のデバイス プロパティでは、対応するシステム定義のレジストリ エントリの値があります。 対応するレジストリ エントリを持つデバイス プロパティの値を使用して、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)対応するレジストリを追加するエントリの値は、対応するデバイスのプロパティを設定します。 同様を使用して、 [ **INF してディレクティブ**](inf-delreg-directive.md)レジストリ エントリの値を削除する対応するデバイスのプロパティを削除します。

たとえば、次**AddReg**ディレクティブは、設定、 **DeviceCharacteristics**レジストリ エントリの値とデバイスの対応する DEVPKEY_Device_Characteristics プロパティ インスタンス化されています。"Abc_Device_Install.HW"セクションでインストールされます。

```ini
[Abc_Device_Install.HW]
...
AddReg = Xxx_AddReg
...
[Xxx_AddReg]
...
[HKR,,DeviceCharacteristics,0x10001,0x00000001
] 
```

### <a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-reg"></a>INF AddReg ディレクティブとカスタム レジストリ エントリの値を変更する INF してディレクティブ

Windows Vista およびそれ以降のバージョンのサポートを使用して、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)と[ **INF してディレクティブ**](inf-delreg-directive.md)ユーザー設定を変更するにはカスタムのデバイス プロパティを表すレジストリ エントリの値。 ただし、カスタム レジストリ エントリの値を表すデバイスのプロパティの作成は、統一されたデバイス プロパティのモデルではサポートされていません。 デバイスのカスタムのレジストリ エントリの値を作成する場合は、Windows Server 2003、Windows XP、および Windows 2000 を管理するよう、同じ方法でレジストリ エントリの値を管理する必要があります。 カスタムのデバイスのプロパティの管理を簡素化するには、カスタムのレジストリ エントリの値を作成する代わりにカスタムのデバイス プロパティを表すプロパティのキー デバイスを作成する必要があります。









