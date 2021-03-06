---
title: gc (条件付きブレークポイントからの実行)
description: Gc コマンドでは、ブレークポイントにヒットします (ステップ実行、トレース、または自由に実行) に使用されたのと同じ方法で条件付きブレークポイントから再開されます。
ms.assetid: 7850269a-3fc7-48b6-a369-bb020a5e11c3
keywords:
- gc (条件付きブレークポイントから移動) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gc (Go from Conditional Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 79095e76fcd3a683ed45e2ab7511c86d9a6e92f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347098"
---
# <a name="gc-go-from-conditional-breakpoint"></a>gc (条件付きブレークポイントからの実行)


**Gc**コマンドは、ブレークポイントにヒットします (ステップ実行、トレース、または自由に実行) に使用されたのと同じ方法で条件付きブレークポイントから実行を再開します。

```dbgcmd
gc
```

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
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

関連するコマンドの概要については、次を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>注釈
-------

ときに、[条件付きブレークポイント](setting-a-conditional-breakpoint.md)実行コマンドが含まれています最後に、このアカウントは、 **gc**コマンド。

たとえば、適切な条件付きブレークポイントの構成は、次のように。

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'gc' " 
```

このブレークポイントに達するし、式が false、使用されていた同じ実行の種類を使用して実行が再開されます。 使用する場合など、 **g (移動)** このブレークポイントに到達するコマンドを自由に実行を再開します。 ただし、ステップまたはトレースの実行を再開するには、ステップ実行か、トレース中にこのブレークポイントに達すると。

その一方で、以下は、不適切なブレークポイント構成では、ブレークポイントに到達する前にステップ インされていた場合でも、実行は自由に再開常にあるため。

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'g' " 
```

 

 





