---
title: Hyper-V 拡張可能スイッチ インスタンスの列挙
description: Hyper-V 拡張可能スイッチ インスタンスの列挙
ms.assetid: 1C4FE71E-689C-4BE8-BDA8-FFC318E37A26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15997e27d231ecce3ee179c8c71102900561f327
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379423"
---
# <a name="enumerating-hyper-v-extensible-switch-instances"></a>Hyper-V 拡張可能スイッチ インスタンスの列挙


[Get-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch) PowerShell コマンドレットが作成されている HYPER-V 仮想ネットワークを列挙します。 1 つ以上の HYPER-V 子パーティションは、各仮想ネットワークに割り当てることができます。 HYPER-V の仮想化スタックは、ネットワークに割り当てられている最初の HYPER-V 子パーティションが開始されると、仮想ネットワークの HYPER-V 拡張可能スイッチのインスタンスを作成します。

[Get-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch)コマンドレットは、次の構文を使用します。

``` syntax
Get-VMSwitch [[-Name] <string>] [-SwitchType <VMSwitchType[]>] [[-ResourcePoolName] <string[]>] [-ComputerName
    <string[]>] [<CommonParameters>]

Get-VMSwitch [[-Id] <Guid[]>] [-SwitchType <VMSwitchType[]>] [[-ResourcePoolName] <string[]>] [-ComputerName
    <string[]>] [<CommonParameters>]
```

次の例からの出力を示しています、 [Get-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch)コマンドレット。

``` syntax
PS C:\Windows\system32> Get-VMSwitch

Name                           Learnable Status
                               Addresses
----                           --------- ------
Virtual Network - 1            2048      {OK}
Virtual Network - 2            2048      {OK}
```

## <a name="related-topics"></a>関連トピック


[Get-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch)

[**Msvm\_VirtualEthernetSwitch**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-virtualethernetswitch)

 

 






