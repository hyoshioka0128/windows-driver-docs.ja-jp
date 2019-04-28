---
title: Hyper-V 拡張可能スイッチ拡張機能の有効化
description: Hyper-V 拡張可能スイッチ拡張機能の有効化
ms.assetid: 13FD68CB-8F50-4BE3-8822-03464D8C118C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1a3a90dcff5d00d692ca2d4598d2b3568e05ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372499"
---
# <a name="enabling-hyper-v-extensible-switch-extensions"></a>Hyper-V 拡張可能スイッチ拡張機能の有効化


HYPER-V 拡張可能スイッチの拡張機能がインストールされているときに、拡張可能スイッチの各インスタンスにバインドされます。 ただし、拡張機能は既定で無効になっている、拡張可能スイッチのインスタンスごとに明示的に有効にする必要があります。

[有効にする VMSwitchExtension](https://technet.microsoft.com/library/hh848541.aspx) PowerShell コマンドレット、拡張可能スイッチの特定のインスタンスで拡張機能を有効にします。 このコマンドレットは、次の構文を使用します。

``` syntax
Enable-VMSwitchExtension [-Name] <string[]> [-ComputerName <string[]>] [<CommonParameters>]

Enable-VMSwitchExtension [-Name] <string[]> [-VMSwitchName] <string[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Enable-VMSwitchExtension [-Name] <string[]> [-VMSwitch] <VMSwitch[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Enable-VMSwitchExtension [-VMSwitchExtension] <VMSwitchExtension[]> [-ComputerName <string[]>] [<CommonParameters>]
```

有効にする VMSwitchExtension コマンドレットを使用する方法の例を次に示します。

``` syntax
PS C:\Windows\system32> Enable-VMSwitchExtension "Switch Extensibility Test Extension 1" PrivateNetwork

PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork "Switch Extensibility Test Extension 1" | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : True
```

**注**  Windows Filtering Platform (WFP) ボックスでフィルター処理拡張機能 (Wfplwfs.sys) は、拡張可能スイッチのインスタンスごとに既定で有効です。

 

## <a name="related-topics"></a>関連トピック


[Enable-VMSwitchExtension](https://technet.microsoft.com/library/hh848541.aspx)

[Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx)

[**Msvm\_EthernetSwitchExtension**](https://msdn.microsoft.com/library/hh850139)

 

 






