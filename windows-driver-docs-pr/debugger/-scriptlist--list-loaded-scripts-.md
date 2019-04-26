---
title: .scriptlist (読み込まれたスクリプトの一覧表示)
description: .Scriptlist コマンドは、読み込まれたスクリプトを一覧表示します。
ms.assetid: 98F24BE6-3F34-44E7-9546-3D5AB6D521DD
keywords:
- .scriptlist (読み込まれたスクリプトを一覧表示) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptlist (List Loaded Scripts)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85dba9f144d77400de63d6ba9b15f414d4c6ffb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338857"
---
# <a name="scriptlist-list-loaded-scripts"></a>.scriptlist (読み込まれたスクリプトの一覧表示)


**.Scriptlist**コマンドが読み込まれたスクリプトを一覧表示します。

```dbgcmd
.scriptlist 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______________"></span>    
なし

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
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

.Scriptlist コマンドには、.scriptload コマンドを使用して読み込まれているすべてのスクリプトが一覧表示します。

.Scriptload を使用して、TestScript が読み込み成功した場合、.scriptlist コマンドは、読み込まれたスクリプトの名前を表示します。

```dbgcmd
0:000> .scriptlist
Command Loaded Scripts:
    JavaScript script from 'C:\WinDbg\Scripts\TestScript.js'
```

**必要条件**

.Script コマンドのいずれかを使用するのには、スクリプトのプロバイダーが読み込まれる必要があります。 使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[**.scriptload (スクリプトの読み込み)**](-scriptload--load-script-.md)

 

 






