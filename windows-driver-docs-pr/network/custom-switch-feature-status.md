---
title: カスタムのスイッチ機能の状態
description: カスタムのスイッチ機能の状態
ms.assetid: 2362EE05-9CC9-451D-80D1-C18CC9274BAB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5efba9e9f5e2dbb0c7731998a1164bdc74feaa34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531157"
---
# <a name="custom-switch-feature-status"></a>カスタムのスイッチ機能の状態


HYPER-V プラットフォームおよび HYPER-V 拡張可能スイッチのインターフェイスは、拡張可能スイッチには、カスタム状態情報を取得するためのインフラストラクチャを提供します。 この情報と呼ばれる*機能の状態を切り替える*情報。

カスタムのスイッチ機能の状態の定義は、管理オブジェクト フォーマット (MOF) クラス定義を使用して、WMI 管理層に登録されます。 カスタムのスイッチ機能の状態の定義の属性を定義する構造体のメンバーだけでなく、MOF クラスの次も場合があります。

-   カスタムのスイッチ機能の状態の定義を一意に識別するための UUID。

-   拡張可能スイッチ拡張機能を一意に識別する GUID。 この GUID として宣言されて、 **ExtensionId**修飾子、MOF ファイルのクラスし、の値に一致する必要があります、 **NetCfgInstanceId**拡張機能の INF ファイルで宣言されているエントリ。

-   わかりやすいクラス名の文字列。 ベンダーの名前は、文字列に含める必要があります。

拡張可能スイッチのカスタム機能の状態の定義については、MOF クラスの例を次に示します。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic,
  UUID("B3E57D77-8E95-4977-97DE-524F8DAF03E4"),
  ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
  Provider("VmmsWmiInstanceAndMethodProvider"), 
  InterfaceVersion("1"),
  InterfaceRevison("0"),
  Locale(0x409),
  Description(
   "Fabricam, Inc. Switch custom feature status description.") : Amended,
  DisplayName("Fabricam, Inc. Switch custom feature status friendly name.") : Amended]
class Fabrikam_CustomSwitchData  : Msvm_EthernetSwitchFeatureSettingData{
    [ Read,
       Write,
       WmiDataId(1),
       InterfaceVersion("1"),
       InterfaceRevision("0"),
       Description(
         "The current status of custom feature on this switch.") : Amended]
     uint32 CurrentStatus = 0 ;
};
```

拡張可能スイッチのカスタム機能の状態の定義については、MOF クラスは、MOF コンパイラ (Mofcomp.exe) を使用して、一般的な情報 model (CIM) リポジトリに登録されます。 登録されると、MOF クラスは、PowerShell コマンドレットと WMI ベースのアプリケーションを構成できます。

次の例では、ファイルを登録する入力する必要があります (Fabrikam\_CustomSwitchData.mof) カスタム スイッチ機能の状態の定義については、MOF クラスを格納しています。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_CustomSwitchData.mof
net start vmms
```

MOF コンパイラを使用する方法の詳細については、次を参照してください。[ドライバーの MOF ファイルをコンパイルする](https://msdn.microsoft.com/library/windows/hardware/ff542012)します。

次の例では、スイッチのデータを取得するカスタム スイッチ機能の状態の定義を使用する方法を示します。 この例では、Fabrikam\_CustomSwitchData MOF クラスを使用して"TestSwitch"という名前のスイッチからスイッチの状態を取得します。 Fabrikam, Inc. の拡張機能では、vSwitch"TestSwitch"が有効になり、123 の状態を返すことができます。

```PowerShell
PS C:\> $switchData = Get-VMSwitchExtensionSwitchData -SwitchName TestSwitch -FeatureId B3E57D77-8E95-4977-97DE-524F8DAF03E4
# Output the current value
PS C:\> $switchData$customSwitchData.Data.CurrentStatus
123
```

スイッチ拡張機能を拡張する方法の詳細については、スイッチ機能の状態情報を管理しを参照してください[を管理するカスタム スイッチ機能の状態の情報](managing-custom-switch-feature-status-information.md)します。

 

 





