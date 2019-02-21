---
title: Windows Vista より前に、のデバイス プロパティを変更する INF ファイル エントリの値
description: Windows Vista より前に、のデバイス プロパティを変更する INF ファイル エントリの値
ms.assetid: b2a1f265-fc9b-47fb-83af-b4f66d79da83
keywords:
- デバイスのプロパティを変更する、WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 162ef532419035b1434bce610760afd25745122f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551087"
---
# <a name="inf-file-entry-values-that-modify-device-properties-before-windows-vista"></a>Windows Vista より前に、のデバイス プロパティを変更する INF ファイル エントリの値


以下は、Windows Server 2003、Windows XP、および Windows 2000 でデバイスのプロパティを変更する INF ファイル エントリの値です。

-   デバイスのプロパティを設定する INF ファイル エントリの値に対応して、[デバイスのシステム定義プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff553413)はの一部である、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)Windows Vista およびそれ以降のバージョンのWindows。

-   [**INF AddReg ディレクティブ**](inf-addreg-directive.md)と[ **INF してディレクティブ**](inf-delreg-directive.md)設定またはデバイスのシステム定義のプロパティに対応するシステム定義のレジストリ エントリの値を削除します。Windows Vista およびそれ以降のバージョンで統一されたデバイス プロパティのモデルの一部であります。

-   INF **AddReg**ディレクティブと INF**して**ディレクティブが設定またはカスタムのデバイスのプロパティに対応するカスタム レジストリ エントリの値を削除します。

概要については、INF ファイルのセクションでは、デバイスのインスタンスをインストールする[デバイス セットアップ クラス](device-setup-classes.md)、[デバイス インターフェイス クラス](device-interface-classes.md)、し、デバイスのインターフェイスは、次のトピックを参照してください。

[**INF *DDInstall*セクション**](inf-ddinstall-section.md)

[**INF ClassInstall32 セクション**](inf-classinstall32-section.md)

[**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)

[**INF *DDInstall*します。インターフェイス セクション**](inf-ddinstall-interfaces-section.md)

### <a href="" id="inf-file-entry-values-that-correspond-to-system-defined-device-propert"></a>デバイスのシステム定義のプロパティに対応する INF ファイル エントリの値

いくつかの INF ファイル エントリの値は、Windows はデバイス インスタンスのプロパティとデバイスのインターフェイスのプロパティに対応するエントリの値をシステム定義のレジストリに設定を使用して情報を提供します。 次に、このような INF ファイル エントリの値によって提供されるレジストリ エントリの値のいくつかの例を示します。

-   [ **INF モデル セクション**](inf-models-section.md) 、INF にはファイルが含まれています、*デバイス説明*エントリの値。 この値に対応、 [ **DEVPKEY_Device_DeviceDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff542407)統一されたデバイス プロパティのプロパティをモデルし、呼び出すことによって取得できる[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)と設定、*プロパティ*SPDRP_DEVICEDESC パラメーター。

-   INF**クラス**のディレクティブを[ **INF バージョン セクション**](inf-version-section.md)が含まれています、*クラス名*エントリの値をの名前を提供する[デバイス セットアップ クラス](device-setup-classes.md)します。 この値に対応、 [ **DEVPKEY_DeviceClass_ClassName** ](https://msdn.microsoft.com/library/windows/hardware/ff542272)統一されたデバイス プロパティのモデルのプロパティ。 呼び出してデバイス セットアップ クラスのクラス名を取得できる[ **SetupDiClassNameFromGuid**](https://msdn.microsoft.com/library/windows/hardware/ff550947)、呼び出すことによって、デバイスのインスタンスのクラス名を取得できると[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)と設定、*プロパティ*SPDRP_CLASS パラメーター。

-   [ **INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)が含まれています、 *InterfaceClassGuid*デバイス インターフェイスの GUID を提供するエントリの値。 この値は、統一されたデバイス プロパティのモデルで DEVPKEY_DeviceInterface_ClassGuid プロパティに対応します。 クラスのルートを呼び出すことによって開くことができるインターフェイス キーのサブキーのクエリを実行して取得できるインストール済みのデバイスのインターフェイスの Guid [ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067) の設定*ClassGuid*パラメーターを**NULL**と*フラグ*DIOCR_INTERFACE パラメーター。 デバイス インターフェイスの GUID を呼び出すことによって取得できる[ **SetupDiEnumDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff551015)、どの取得、 [ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)デバイス インスタンスに関連付けられているデバイスのインターフェイスの構造体。 **InterfaceClassGuid** SP_DEVICE_INTERFACE_DATA 構造体のメンバーがインターフェイス クラス GUID を識別します。

### <a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-def"></a>INF AddReg ディレクティブとデバイスのシステム定義のプロパティを変更する INF してディレクティブ

多くのシステム定義のデバイス プロパティでは、対応するシステム定義のレジストリ エントリの値があります。 デバイスのプロパティを使用して、対応するレジストリ エントリ値を持つ、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)対応するレジストリを追加するエントリの値は、対応するデバイスのプロパティを設定します。 同様を使用して、 [ **INF してディレクティブ**](inf-delreg-directive.md)を対応するレジストリを削除するエントリの値では、対応するデバイスのプロパティも削除されます。

INF など**AddReg** "Abc_Device_Install.HW"セクションの設定は、次のディレクティブ、 **DeviceCharacteristics**デバイス インスタンスのレジストリ エントリの値。

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

**DeviceCharacteristics**レジストリ エントリの値に対応して、 [ **DEVPKEY_Device_Characteristics** ](https://msdn.microsoft.com/library/windows/hardware/ff542375)プロパティ、[統一されたデバイスプロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)Windows Vista および Windows の以降のバージョン。

### <a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-reg"></a>INF AddReg ディレクティブとカスタム レジストリ エントリの値を変更する INF してディレクティブ

Windows では、システム定義のレジストリ エントリの値とデバイスのシステム定義のプロパティ間の通信を管理します。 ただし、Windows では、カスタムのレジストリ エントリの値とカスタムのデバイスのプロパティ間の通信は管理しません。 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)または[ **INF してディレクティブ**](inf-delreg-directive.md)カスタムを変更するレジストリ エントリの値には影響しません、Windows を管理するシステム定義のプロパティ。

次の例に示すように設定されているデバイスのカスタム インスタンスのプロパティを呼び出すことによって取得できる[ **SetupDiGetCustomDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551099)します。

```ini
[XxxDDInstall.HW]
...
AddReg = Xxx_AddReg
...
[Xxx_AddReg]
...
[HKR,,CustomPropertyName,0x10001,0x00000001
] 
```

対応するカスタム レジストリ エントリの値を持つカスタムのデバイスのプロパティにアクセスする方法の詳細については、次を参照してください。[へのアクセスのカスタム デバイス プロパティ](accessing-custom-device-properties.md)します。









