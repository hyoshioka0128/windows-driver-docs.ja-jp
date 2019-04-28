---
title: Hyper-V 拡張可能スイッチ拡張機能の無効化
description: Hyper-V 拡張可能スイッチ拡張機能の無効化
ms.assetid: 3BE5A53E-3F74-4B99-B504-5D7F090343E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24381583612412642f2566e274f192b1497874b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379568"
---
# <a name="disabling-hyper-v-extensible-switch-extensions"></a>Hyper-V 拡張可能スイッチ拡張機能の無効化


[Disable-vmswitchextension](https://technet.microsoft.com/library/hh848545.aspx) PowerShell コマンドレットは、拡張可能スイッチの特定のインスタンスで拡張機能を無効にします。

[Disable-vmswitchextension](https://technet.microsoft.com/library/hh848545.aspx)コマンドレットは、次の構文を使用します。

``` syntax
Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-ComputerName <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitchName] <string[]> [-ComputerName
    <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitch] <VMSwitch[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtension] <VMSwitchExtension[]> [-ComputerName <string[]>]
    [<CommonParameters>]
```

使用する方法の例を次に示します、 [Disable-vmswitchextension](https://technet.microsoft.com/library/hh848545.aspx)コマンドレット。

``` syntax
PS C:\Windows\system32> Disable-VMSwitchExtension "Switch Extensibility Test Extension 1" PrivateNetwork

PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork "Switch Extensibility Test Extension 1" | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False
```

## <a name="related-topics"></a>関連トピック


[Disable-vmswitchextension](https://technet.microsoft.com/library/hh848545.aspx)

[Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx)

[**Msvm\_EthernetSwitchExtension**](https://msdn.microsoft.com/library/hh850139)

 

 






