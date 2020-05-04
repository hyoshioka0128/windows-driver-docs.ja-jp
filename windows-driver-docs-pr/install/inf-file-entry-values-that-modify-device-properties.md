---
title: Windows Vista より前にデバイスのプロパティを変更する INF ファイルエントリ値
description: Windows Vista より前にデバイスのプロパティを変更する INF ファイルエントリ値
ms.assetid: b2a1f265-fc9b-47fb-83af-b4f66d79da83
keywords:
- デバイスのプロパティ WDK デバイスのインストール、変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64d99683a14a399284ae7b1c995484179661c8ed
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223150"
---
# <a name="inf-file-entry-values-that-modify-device-properties-before-windows-vista"></a>Windows Vista より前にデバイスのプロパティを変更する INF ファイルエントリ値


Windows Server 2003、Windows XP、および Windows 2000 のデバイスプロパティを変更する INF ファイルエントリ値を次に示します。

-   Windows Vista 以降のバージョンの Windows で、統合された[デバイスのプロパティモデル](unified-device-property-model--windows-vista-and-later-.md)に含まれる[システム定義のデバイス](https://docs.microsoft.com/previous-versions/ff553413(v=vs.85))プロパティに対応するデバイスプロパティを設定する INF ファイルエントリ値。

-   [**Inf AddReg ディレクティブ**](inf-addreg-directive.md)および[**inf delreg ディレクティブ**](inf-delreg-directive.md)。システム定義のレジストリエントリの値を設定または削除します。この値は、Windows Vista 以降のバージョンで統合されたデバイスのプロパティモデルに含まれるシステム定義のデバイスプロパティに対応します。

-   INF **AddReg**ディレクティブと Inf **delreg**ディレクティブ。カスタムのデバイスプロパティに対応するカスタムレジストリエントリ値を設定または削除します。

デバイスインスタンス、[デバイスセットアップクラス](device-setup-classes.md)、[デバイスインターフェイスクラス](device-interface-classes.md)、デバイスインターフェイスをインストールする INF ファイルのセクションに関する一般的な情報については、次のトピックを参照してください。

[**INF *Ddinstall*セクション**](inf-ddinstall-section.md)

[**INF ClassInstall32 セクション**](inf-classinstall32-section.md)

[**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)

[**INF *Ddinstall*。インターフェイスセクション**](inf-ddinstall-interfaces-section.md)

### <a name="inf-file-entry-values-that-correspond-to-system-defined-device-properties"></a><a href="" id="inf-file-entry-values-that-correspond-to-system-defined-device-propert"></a>システム定義のデバイスプロパティに対応する INF ファイルエントリ値

一部の INF ファイルエントリの値は、デバイスインスタンスのプロパティとデバイスインターフェイスのプロパティに対応するシステム定義のレジストリエントリの値を設定するために Windows が使用する情報を提供します。 次に、このような INF ファイルエントリ値によって提供されるレジストリエントリ値の例をいくつか示します。

-   INF ファイルの [ [**Inf モデル] セクション**](inf-models-section.md)には、*デバイスの説明*のエントリ値が含まれます。 この値は、統合されたデバイスプロパティモデルの[**DEVPKEY_Device_DeviceDesc**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-devicedesc)プロパティに対応しており、 [**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)を呼び出して*プロパティ*パラメーターを SPDRP_DEVICEDESC に設定することによって取得できます。

-   [**Inf バージョンセクション**](inf-version-section.md)の inf**クラス**ディレクティブには、[デバイスセットアップクラス](device-setup-classes.md)の名前を指定する*クラス名*エントリ値が含まれています。 この値は、統合されたデバイスプロパティモデルの[**DEVPKEY_DeviceClass_ClassName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-classname)プロパティに対応します。 デバイスセットアップクラスのクラス名は、 [**SetupDiClassNameFromGuid**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida)を呼び出すことによって取得できます。デバイスインスタンスのクラス名は、 [**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)を呼び出して*プロパティ*パラメーターを SPDRP_CLASS に設定することによって取得できます。

-   [**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)には、デバイスインターフェイスの GUID を提供する*InterfaceClassGuid*エントリ値が含まれています。 この値は、統合されたデバイスプロパティモデルの DEVPKEY_DeviceInterface_ClassGuid プロパティに対応します。 インストールされているデバイスインターフェイスクラスの Guid を取得するには、インターフェイスキーのルートのサブキーを照会します。これは、 [**Setupdiopenclassregkeyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)を呼び出すことによって開くことができます。また、 *Classguid*パラメーターを**NULL**に設定し、 *Flags*パラメーターを DIOCR_INTERFACE に設定することもできます。 デバイスインターフェイスの GUID は、 [**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)を呼び出すことによって取得できます。このインターフェイスは、デバイスインスタンスに関連付けられているデバイスインターフェイスの[**SP_DEVICE_INTERFACE_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)構造を取得します。 SP_DEVICE_INTERFACE_DATA 構造体の**InterfaceClassGuid**メンバーは、インターフェイスクラス GUID を識別します。

### <a name="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-defined-device-properties"></a><a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-def"></a>INF AddReg ディレクティブと INF DelReg ディレクティブ (システム定義のデバイスプロパティを変更する)

システム定義のデバイスプロパティの多くには、対応するシステム定義のレジストリエントリ値があります。 対応するレジストリエントリ値を持つデバイスプロパティの場合、 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)を使用して対応するレジストリエントリ値を追加すると、対応するデバイスプロパティが設定されます。 同様に、 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)を使用して、対応するレジストリエントリ値を削除すると、対応するデバイスプロパティも削除されます。

たとえば、次の "Abc_Device_Install" セクションの INF **AddReg**ディレクティブは、デバイスインスタンスの**DeviceCharacteristics**レジストリエントリの値を設定します。

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

**DeviceCharacteristics**レジストリエントリの値は、windows Vista 以降のバージョンの windows では、統合された[デバイスプロパティモデル](unified-device-property-model--windows-vista-and-later-.md)の[**DEVPKEY_Device_Characteristics**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-characteristics)プロパティに対応しています。

### <a name="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-registry-entry-values"></a><a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-reg"></a>カスタムレジストリエントリ値を変更する INF AddReg ディレクティブおよび INF DelReg ディレクティブ

Windows は、システム定義のレジストリエントリ値とシステム定義のデバイスプロパティの対応を管理します。 ただし、Windows では、カスタムレジストリエントリ値とカスタムデバイスプロパティの対応は管理しません。 [**Inf AddReg ディレクティブ**](inf-addreg-directive.md)、またはカスタムレジストリエントリ値を変更する[**inf delreg ディレクティブ**](inf-delreg-directive.md)は、Windows が管理するシステム定義のプロパティには影響しません。

次の例に示すように設定されているカスタムデバイスインスタンスのプロパティは、 [**SetupDiGetCustomDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetcustomdevicepropertya)を呼び出すことによって取得できます。

```inf
[XxxDDInstall.HW]
...
AddReg = Xxx_AddReg
...
[Xxx_AddReg]
...
[HKR,,CustomPropertyName,0x10001,0x00000001
] 
```

対応するカスタムレジストリエントリ値を持つカスタムデバイスプロパティにアクセスする方法の詳細については、「[カスタムデバイスプロパティ](accessing-custom-device-properties.md)へのアクセス」を参照してください。









