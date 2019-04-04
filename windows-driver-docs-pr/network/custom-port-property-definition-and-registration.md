---
title: カスタム ポート プロパティの定義と登録
description: カスタム ポート プロパティの定義と登録
ms.assetid: 55FCA402-191B-4DC9-A126-77AA15183E90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00801e7d5a61dcf5c0b7e570c7a40704a7796d29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579463"
---
# <a name="custom-port-property-definition-and-registration"></a>カスタム ポート プロパティの定義と登録


HYPER-V 拡張可能スイッチのポートのポリシーのカスタム プロパティ定義は、管理オブジェクト フォーマット (MOF) クラス定義を使用して、WMI 管理層に登録されます。 カスタム ポートのプロパティの属性を定義する構造体のメンバーだけでなく、MOF クラスの次も場合があります。

-   カスタム ポートのプロパティを一意に識別するための UUID。

-   拡張可能スイッチ拡張機能を一意に識別する GUID。 この GUID として宣言されて、 **ExtensionId**修飾子、MOF ファイルのクラスし、の値に一致する必要があります、 **NetCfgInstanceId**拡張機能の INF ファイルで宣言されているエントリ。

-   わかりやすいクラス名の文字列。 ベンダーの名前は、文字列に含める必要があります。

拡張可能スイッチ ポートのポリシーのカスタム プロパティの MOF クラスの例を次に示します。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic, 
 UUID("EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB"),
 ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
 Provider("VmmsWmiInstanceAndMethodProvider"), 
 Locale(0x409),
 InterfaceVersion("1"),
 InterfaceRevison("0"),
DisplayName("Fabrikam, Inc. Port Settings Friendly Name") : Amended,
Description("Fabrikam, Inc. Port Settings detailed description.") : Amended]
class Fabrikam_PortCustomSettingData : Msvm_EthernetSwitchPortFeatureSettingData {
   
    [ Read,
      Write,
      WmiDataId(1),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
      Description (
         "int32 setting.") : Amended]
    uint32 SettingIntA = 0;

    [ Read,
      Write,
      WmiDataId(2),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
      Description (
         "int64 setting.") : Amended]
    uint64 SettingIntB = 0;
};
```

ポートのポリシーのカスタム プロパティ用の MOF クラスは、MOF コンパイラ (Mofcomp.exe) を使用して、一般的な情報 model (CIM) リポジトリに登録されます。 登録されると、MOF クラスは、PowerShell コマンドレットと WMI ベースのアプリケーションを構成できます。

次の例では、ファイルを登録する入力する必要があります (Fabrikam\_PortCustomSettingData.mof) MOF クラスをカスタム ポートのプロパティを格納します。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_PortCustomSettingData.mof
net start vmms
```

MOF コンパイラを使用する方法の詳細については、[ドライバーの MOF ファイルをコンパイルする](https://msdn.microsoft.com/library/windows/hardware/ff542012)を参照してください。

次の例では、サンプルの機能を構成する方法を示します。 この例では、Fabrikam\_PortCustomSettingData MOF クラスは、"TestVm"という名前の HYPER-V パーティションからのポートを構成するために使用します。

```PowerShell
# Retrieve the template object for the custom configuration. We know the ID already so
# we can retrieve it directly, otherwise Get-VmSystemSwitchExtensionPortFeature can list all available
# properties. 
PS C:\> $feature = Get-VMSystemSwitchExtensionPortFeature -FeatureId EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB

# Output the values
PS C:\> $feature

Id            : eb29f0f2-f5dc-45c6-81bb-3cd9f219bbbb
ExtensionId   : 5cbf81bd-5055-47cd-9055-a76b2b4e369d
ExtensionName : Fabrican Extension
Name          : Fabrikam, Inc. Port Settings Friendly Name
ComputerName  : TEST_SERVER
SettingData   : \\TEST_SERVER\root\virtualization\v2:VendorName_SwitchPortCustomSettingData.InstanceID="Microsoft:Defini
                tion\\EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB\\Default"

# Cast the SettingsData to a WMI object to see the actual configurable values. 
PS C:\> $wmiObj = [wmi]$feature.SettingData
PS C:\> $wmiObj

__GENUS          : 2
__CLASS          : Fabrikam_PortCustomSettingData
__SUPERCLASS     : Msvm_EthernetSwitchFeatureSettingData
__DYNASTY        : CIM_ManagedElement
__RELPATH        : Fabrikam_PortCustomSettingData.InstanceID="Microsoft:Definition\\EB29F0F2-F5DC-45C6-81BB-3CD
                   9F219BBBB\\Default"
__PROPERTY_COUNT : 6
__DERIVATION     : {Msvm_EthernetSwitchFeatureSettingData, CIM_SettingData, CIM_ManagedElement}
__SERVER         : TEST_SERVER
__NAMESPACE      : root\virtualization\v2
__PATH           : \\TEST_SERVER\root\virtualization\v2:Fabrikam_PortCustomSettingData.InstanceID="Microsoft:Def
                   inition\\EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB\\Default"
Caption          : Fabrikam, Inc. Port Settings Friendly Name
Description      : Fabrikam, Inc. Port Settings detailed description.
ElementName      : Fabrikam, Inc. Port Settings Friendly Name
InstanceID       : Microsoft:Definition\EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB\Default
SettingIntA      : 0
SettingIntB      : 0

# Update the property settings and add to the NIC attached to TestVm
PS C:\> $wmiObj.SettingIntA = 100
PS C:\> $wmiObj.SettingIntB = 9999
PS C:\> Add-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $feature -VmName TestVm
 
# Validate that the properties are now set on the VM’s NIC
PS C:\> $feature = Get-VmSwitchExtensionPortFeature -FeatureId EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB -VmName TestVm

PS C:\> [wmi]$feature.SettingData


__GENUS          : 2
__CLASS          : Fabrikam_PortCustomSettingData
__SUPERCLASS     : Msvm_EthernetSwitchFeatureSettingData
__DYNASTY        : CIM_ManagedElement
__RELPATH        : Fabrikam_PortCustomSettingData.InstanceID="Microsoft:6208FB20-2490-4DC1-B121-877B68B4CE11\\4
                   DDC57F5-6DAE-4A36-9D62-7A838D5601F2\\C\\EB29F0F2-F5DC-45C6-81BB-3CD9F219BBBB\\CB323B56-FA54-4506-B58
                   B-78C70C0B3229"
__PROPERTY_COUNT : 6
__DERIVATION     : {Msvm_EthernetSwitchFeatureSettingData, CIM_SettingData, CIM_ManagedElement}
__SERVER         : TEST_SERVER
__NAMESPACE      : root\virtualization\v2
__PATH           : \\TEST_SERVER\root\virtualization\v2:Fabrikam_PortCustomSettingData.InstanceID="Microsoft:620
                   8FB20-2490-4DC1-B121-877B68B4CE11\\4DDC57F5-6DAE-4A36-9D62-7A838D5601F2\\C\\EB29F0F2-F5DC-45C6-81BB-
                   3CD9F219BBBB\\CB323B56-FA54-4506-B58B-78C70C0B3229"
Caption          : Fabrikam, Inc. Port Settings Friendly Name
Description      : Fabrikam, Inc. Port Settings detailed description.
ElementName      : Fabrikam, Inc. Port Settings Friendly Name
InstanceID       : Microsoft:6208FB20-2490-4DC1-B121-877B68B4CE11\4DDC57F5-6DAE-4A36-9D62-7A838D5601F2\C\EB29F0F2-F5DC-
                   45C6-81BB-3CD9F219BBBB\CB323B56-FA54-4506-B58B-78C70C0B3229
SettingIntA      : 100
SettingIntB      : 9999
```

スイッチ拡張機能を拡張する方法の詳細については、ポートのポリシーの管理を参照してください[ポート ポリシーの管理](managing-port-policies.md)します。

 

 





