---
title: カスタム ポート機能の状態
description: カスタム ポート機能の状態
ms.assetid: 87E88302-6FEA-4D71-A80D-E7AD6D42C0BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34ba24ba8744b3b2814f6a58fd8c2291044207d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326030"
---
# <a name="custom-port-feature-status"></a>カスタム ポート機能の状態


HYPER-V プラットフォームおよび HYPER-V 拡張可能スイッチのインターフェイスは、拡張可能スイッチ ポートのカスタム状態情報を取得するためのインフラストラクチャを提供します。 この情報と呼ばれる*機能の状態をポート*情報。

HYPER-V 拡張可能なスイッチ ポートのプロパティのカスタム機能の状態の定義は、管理オブジェクト フォーマット (MOF) クラス定義を使用して、WMI 管理層に登録されます。 カスタム ポート機能の状態の定義の属性を定義する構造体のメンバーだけでなく、MOF クラスの次も場合があります。

-   カスタム ポート機能の状態の定義を一意に識別するための UUID。

-   拡張可能スイッチ拡張機能を一意に識別する GUID。 この GUID として宣言されて、 **ExtensionId**修飾子、MOF ファイルのクラスし、の値に一致する必要があります、 **NetCfgInstanceId**拡張機能の INF ファイルで宣言されているエントリ。

-   わかりやすいクラス名の文字列。 ベンダーの名前は、文字列に含める必要があります。

拡張可能スイッチのポートのカスタム機能の状態の定義については、MOF クラスの例を次に示します。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic,
  UUID("DAA0B7CC-74DB-41ef-8354-7002F9FA463E"),
  ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
  Provider("VmmsWmiInstanceAndMethodProvider"), 
  InterfaceVersion("1"),
  InterfaceRevison("0"),
  Locale(0x409),
  Description("Fabricam, Inc. port custom feature status description.") : Amended,
  DisplayName("Fabricam, Inc.port custom feature status friendly name.") : Amended]
class Fabrikam_CustomPortData  : Msvm_EthernetPortData {
    [ Read,
       Write,
       WmiDataId(1),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
       Description(
         "The current status of custom feature on this port.") : Amended]
     uint32 CurrentStatus = 0 ;
};
```

ポートのカスタム機能の状態の定義については、MOF クラスは、MOF コンパイラ (Mofcomp.exe) を使用して、一般的な情報 model (CIM) リポジトリに登録されます。 登録されると、MOF クラスは、PowerShell コマンドレットと WMI ベースのアプリケーションを構成できます。

次の例では、ファイルを登録する入力する必要があります (Fabrikam\_CustomPortData.mof) カスタム ポート機能の状態の定義については、MOF クラスを格納しています。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_CustomPortData.mof
net start vmms
```

MOF コンパイラを使用する方法の詳細については、次を参照してください。[ドライバーの MOF ファイルをコンパイルする](https://msdn.microsoft.com/library/windows/hardware/ff542012)します。

次の例では、ポートのデータを取得するカスタム ポート機能の状態の定義を使用する方法を示します。 この例では、Fabrikam\_CustomPortData MOF クラスを使用して"TestVm"という名前の HYPER-V パーティションからポートの状態を取得します。 Fabrikam, Inc. の拡張機能では、vSwitch"TestSwitch"が有効になり、123 の状態を返すことができます。

```PowerShell
PS C:\> $portData = Get-VMSwitchExtensionPortData -VmName TestVm -FeatureId DAA0B7CC-74DB-41ef-8354-7002F9FA463E
# Output the current value
PS C:\> $portData.Data.CurrentStatus
123
```

スイッチ拡張機能を拡張する方法の詳細については、管理ポート機能の状態情報を参照してください[カスタム ポートの機能の状態情報を管理する](managing-custom-port-feature-status-information.md)します。

 

 





