---
title: .kdtargetmac (ターゲットの MAC アドレスの表示)
description: 表示対象の MAC アドレスです。
ms.assetid: 95042682-BD92-44B0-AAA8-AB8661393230
keywords:
- .kdtargetmac (表示対象の MAC アドレス) の Windows デバッグ
ms.date: 05/21/2018
topic_type:
- apiref
api_name:
- .kdtargetmac (Display Target MAC Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f8c92bc89fa5ba62ce8aca2a33240b6761eb9444
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538058"
---
# <a name="kdtargetmac-display-target-mac-address"></a>.kdtargetmac (ターゲットの MAC アドレスの表示)


表示対象の MAC アドレス

```dbgcmd
.kdtargetmac 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

.Kdtargetmac コマンドを使用すると、ターゲット システムの MAC (メディア アクセス制御) のアドレスを表示できます。

```dbgcmd
0: kd> .kdtargetmac 

The target machine MAC address in open-device format is: XXXXXXXXXXXX
```

.Kdtargetmac はコマンドが KDNET がターゲット システムで有効になっている場合に使用できます。 /Dbgsettings オプションを使用して BCDEdit のコマンドを使用すると、ターゲット システムの構成を表示できます。 Debugtype *NET* KDNET が構成されていることを示します。

```dbgcmd
C:\WINDOWS\system32>bcdedit /dbgsettings
key                     1.2.3.4
debugtype               NET
hostip                  192.168.1.10
port                    50000
dhcp                    Yes
The operation completed successfully.
```

詳細については、[KDNET ネットワーク カーネル デバッグ手作業でセットアップ](setting-up-a-network-debugging-connection.md)を参照してください。

<a name="remarks"></a>注釈
-------

ターゲット システムの MAC アドレスがわかっていなくてはネットワークのトレースおよびその他のユーティリティに役立つことができます。

 

 





