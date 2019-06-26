---
title: カスタム スイッチ プロパティの定義と登録
description: カスタム スイッチ プロパティの定義と登録
ms.assetid: DB80E86D-8553-47B5-8AE1-6D430FDDE206
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b206b4d578d3cce6e235fabf53da6bd74cb82df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364954"
---
# <a name="custom-switch-property-definition-and-registration"></a>カスタム スイッチ プロパティの定義と登録


HYPER-V 拡張可能スイッチのポリシーのカスタム プロパティ定義は、管理オブジェクト フォーマット (MOF) クラス定義を使用して、WMI 管理層に登録されます。 スイッチのカスタム プロパティの属性を定義する構造体のメンバーだけでなく、MOF クラスの次も場合があります。

-   スイッチのカスタム プロパティを一意に識別するための UUID。

-   拡張可能スイッチ拡張機能を一意に識別する GUID。 この GUID として宣言されて、 **ExtensionId**修飾子、MOF ファイルのクラスし、の値に一致する必要があります、 **NetCfgInstanceId**拡張機能の INF ファイルで宣言されているエントリ。

-   わかりやすいクラス名の文字列。 ベンダーの名前は、文字列に含める必要があります。

拡張可能スイッチのポリシーのカスタム プロパティの MOF クラスの例を次に示します。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic, 
 UUID("FF36C3A6-D2F1-46ed-A376-32B43D6B8390"),
 ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
 Provider("VmmsWmiInstanceAndMethodProvider"), 
  Locale(0x409),
 InterfaceVersion("1"),
 InterfaceRevison("0"),
DisplayName("Fabrikam, Inc.  Switch Settings Friendly Name") : Amended,
Description("Fabrikam, Inc.  Switch Settings detailed description.") : Amended]
class Fabrikam_SwitchCustomSettingData : Msvm_EthernetSwitchFeatureSettingData {
   
    [ Read,
      Write,
      WmiDataId(1),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
      Description (
         "int32 setting.") : Amended]
    uint32 SwitchSettingIntA = 0;

    [ Read,
      Write,
      WmiDataId(2),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
      Description (
         "int64 setting.") : Amended]
    uint64 SwitchSettingIntB = 0;
};
```

スイッチのポリシーのカスタム プロパティ用の MOF クラスは、MOF コンパイラ (Mofcomp.exe) を使用して、一般的な情報 model (CIM) リポジトリに登録されます。 登録されると、MOF クラスは、PowerShell コマンドレットと WMI ベースのアプリケーションを構成できます。

次の例では、ファイルを登録する入力する必要があります (Fabrikam\_SwitchCustomSettingData.mof) MOF クラスをカスタム ポートのプロパティを格納します。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_SwitchCustomSettingData.mof
net start vmms
```

MOF コンパイラを使用する方法の詳細については、次を参照してください。[ドライバーの MOF ファイルをコンパイルする](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)します。

次の例では、サンプルの機能を構成する方法を示します。 この例では、Fabrikam\_SwitchCustomSettingData MOF クラスは、"TestSwitch"という名前のスイッチを構成するために使用します。

```PowerShell
# Retrieve the template object for the custom configuration. We know the ID already so
# we can retrieve it directly, otherwise Get-VMSystemSwitchExtensionSwitchFeature can list all available
# properties. 
PS C:\> $feature = Get-VMSystemSwitchExtensionSwitchFeature -FeatureId FF36C3A6-D2F1-46ed-A376-32B43D6B8390

# Output the values
PS C:\temp> $feature


Id            : ff36c3a6-d2f1-46ed-a376-32b43d6b8390
ExtensionId   : 5CBF81BE-5055-47CD-9055-A76B2B4E369E
ExtensionName : Fabrican Extension
Name          : Fabrikam, Inc. Switch Settings Friendly Name
ComputerName  : TEST_SERVER
SettingData   : \\TEST_SERVER\root\virtualization\v2:VendorName_SwitchCustomSettingData.InstanceID="Microsoft:Definition\\
                FF36C3A6-D2F1-46ED-A376-32B43D6B8390\\Default"

# Cast the SettingsData to a WMI object to see the actual configurable values. 
PS C:\> $wmiObj = [wmi]$feature.SettingData
PS C:\> $wmiObj


__GENUS           : 2
__CLASS           : Fabrikam_SwitchCustomSettingData 
__SUPERCLASS      : Msvm_EthernetSwitchFeatureSettingData
__DYNASTY         : CIM_ManagedElement
__RELPATH         : Fabrikam_SwitchCustomSettingData .InstanceID="Microsoft:Definition\\FF36C3A6-D2F1-46ED-A376-32B43D
                    6B8390\\Default"
__PROPERTY_COUNT  : 6
__DERIVATION      : {Msvm_EthernetSwitchFeatureSettingData, Msvm_FeatureSettingData, CIM_SettingData,
                    CIM_ManagedElement}
__SERVER          : TEST_SERVER
__NAMESPACE       : root\virtualization\v2
__PATH            : \\TEST_SERVER\root\virtualization\v2:Fabrikam_SwitchCustomSettingData .InstanceID="Microsoft:Definiti
                    on\\FF36C3A6-D2F1-46ED-A376-32B43D6B8390\\Default"
Caption           : Fabrikam, Inc. Switch Settings Friendly Name
Description       : Fabrikam, Inc. Switch Settings detailed description.
ElementName       : Fabrikam, Inc. Switch Settings Friendly Name
InstanceID        : Microsoft:Definition\FF36C3A6-D2F1-46ED-A376-32B43D6B8390\Default
SwitchSettingIntA : 0
SwitchSettingIntB : 0
PSComputerName    : TEST_SERVER

# Update the property settings and add to the NIC attached to TestVm
PS C:\> $wmiObj.SwitchSettingIntA = 100
PS C:\> $wmiObj.SwitchSettingIntB = 9999
PS C:\> Add-VMSwitchExtensionSwitchFeature -VMSwitchExtensionFeature $feature -SwitchName TestSwitch
 
# Validate that the properties are now set on the VM’s NIC
PS C:\> $feature = Get-VmSwitchExtensionSwitchFeature -FeatureId FF36C3A6-D2F1-46ed-A376-32B43D6B8390 -SwitchName TestSwitch

PS C:\> [wmi]$feature.SettingData


__GENUS           : 2
__CLASS           : Fabrikam_SwitchCustomSettingData 
__SUPERCLASS      : Msvm_EthernetSwitchFeatureSettingData
__DYNASTY         : CIM_ManagedElement
__RELPATH         : Fabrikam_SwitchCustomSettingData .InstanceID="Microsoft:88835394-FDE1-437C-B249-D840575154E2\\FF36
                    C3A6-D2F1-46ED-A376-32B43D6B8390\\F9EA07E7-7B73-431A-8705-26EC2B592306"
__PROPERTY_COUNT  : 6
__DERIVATION      : {Msvm_EthernetSwitchFeatureSettingData, Msvm_FeatureSettingData, CIM_SettingData,
                    CIM_ManagedElement}
__SERVER          : TEST_SERVER
__NAMESPACE       : root\virtualization\v2
__PATH            : \\TEST_SERVER\root\virtualization\v2:Fabrikam_SwitchCustomSettingData .InstanceID="Microsoft:88835394
                    -FDE1-437C-B249-D840575154E2\\FF36C3A6-D2F1-46ED-A376-32B43D6B8390\\F9EA07E7-7B73-431A-8705-26EC2B5
                    92306"
Caption           : Fabrikam, Inc. Switch Settings Friendly Name
Description       : Fabrikam, Inc. Switch Settings detailed description.
ElementName       : Fabrikam, Inc. Switch Settings Friendly Name
InstanceID        : Microsoft:88835394-FDE1-437C-B249-D840575154E2\FF36C3A6-D2F1-46ED-A376-32B43D6B8390\F9EA07E7-7B73-4
                    31A-8705-26EC2B592306
SwitchSettingIntA : 100
SwitchSettingIntB : 9999
PSComputerName    : TEST_SERVER
```

スイッチ拡張機能を拡張する方法の詳細については、スイッチのポリシーを管理しを参照してください[スイッチ ポリシーの管理](managing-switch-policies.md)します。

 

 





