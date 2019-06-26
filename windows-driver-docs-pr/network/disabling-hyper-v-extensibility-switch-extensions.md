---
title: Hyper-V 拡張可能スイッチ拡張機能の無効化
description: Hyper-V 拡張可能スイッチ拡張機能の無効化
ms.assetid: 3BE5A53E-3F74-4B99-B504-5D7F090343E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adea2e584806ecd34629958dd88da2a20c066dbc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386570"
---
# <a name="disabling-hyper-v-extensible-switch-extensions"></a>Hyper-V 拡張可能スイッチ拡張機能の無効化


[Disable-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/disable-vmswitchextension) PowerShell コマンドレットは、拡張可能スイッチの特定のインスタンスで拡張機能を無効にします。

[Disable-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/disable-vmswitchextension)コマンドレットは、次の構文を使用します。

``` syntax
Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-ComputerName <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitchName] <string[]> [-ComputerName
    <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitch] <VMSwitch[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtension] <VMSwitchExtension[]> [-ComputerName <string[]>]
    [<CommonParameters>]
```

使用する方法の例を次に示します、 [Disable-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/disable-vmswitchextension)コマンドレット。

``` syntax
PS C:\Windows\system32> Disable-VMSwitchExtension "Switch Extensibility Test Extension 1" PrivateNetwork

PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork "Switch Extensibility Test Extension 1" | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False
```

## <a name="related-topics"></a>関連トピック


[Disable-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/disable-vmswitchextension)

[Get-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension)

[**Msvm\_EthernetSwitchExtension**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

 

 






