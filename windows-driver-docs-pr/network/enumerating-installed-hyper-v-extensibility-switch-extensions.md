---
title: Hyper-V 拡張可能スイッチ拡張機能の列挙
description: Hyper-V 拡張可能スイッチ拡張機能の列挙
ms.assetid: AC468A8F-5C48-419B-9E9E-D63925E1CE9D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 477799f927ef067e391b71dc79d1b7c4f153171d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354582"
---
# <a name="enumerating-hyper-v-extensible-switch-extensions"></a>Hyper-V 拡張可能スイッチ拡張機能の列挙


[Get-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension) PowerShell コマンドレットは、拡張可能スイッチのインスタンスにバインドされている HYPER-V 拡張可能スイッチ拡張機能を列挙します。 このコマンドレットは、拡張可能スイッチのインスタンスで、拡張機能が有効になっているかどうかも報告されます。

[Get-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension)コマンドレットは、次の構文を使用します。

``` syntax
Get-VMSwitchExtension [[-VMSwitchName] <string[]>] [[-Name] <string[]>] [-ComputerName <string[]>]
    [<CommonParameters>]

Get-VMSwitchExtension [[-VMSwitch] <VMSwitch[]>] [-ComputerName <string[]>] [<CommonParameters>]
```

次の例からの出力を示しています、 [Get-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension)コマンドレット。

``` syntax
PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : NDIS Capture LightWeight Filter
ExtensionType : Capture
SwitchName    : PrivateNetwork
Enabled       : False

Name          : Switch Extensibility Test Extension 2
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False

Name          : WFP extensible switch Layers LightWeight Filter
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : True
```

**注**  例では、情報の量を最小限に抑えるためにフィルター コマンド"fl"から返される拡張オブジェクトをパイプ処理します。 これが原因で表示される情報のサブセットでありの属性と一致する、 **-プロパティ**スイッチします。

 

## <a name="related-topics"></a>関連トピック


[Get-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension)

[**Msvm\_EthernetSwitchExtension**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

 

 






