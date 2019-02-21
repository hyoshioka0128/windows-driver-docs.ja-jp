---
title: HYPER-V 拡張可能スイッチの拡張機能を無効にします。
description: HYPER-V 拡張可能スイッチの拡張機能を無効にします。
ms.assetid: 3BE5A53E-3F74-4B99-B504-5D7F090343E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24381583612412642f2566e274f192b1497874b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552671"
---
# <a name="disabling-hyper-v-extensible-switch-extensions"></a>HYPER-V 拡張可能スイッチの拡張機能を無効にします。


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

 

 






