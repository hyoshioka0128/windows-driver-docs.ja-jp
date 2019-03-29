---
title: .scriptproviders (スクリプト プロバイダーの一覧表示)
description: .Scriptproviders コマンドには、アクティブ スクリプトのプロバイダーが一覧表示されます。
ms.assetid: DF2FAA60-422F-4600-9E31-0F8EF127E5A9
keywords:
- .scriptproviders (スクリプト プロバイダーの一覧) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptproviders (List Script Providers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba9ca106317d4f116e36222d75909f51d5f94a4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581348"
---
# <a name="scriptproviders-list-script-providers"></a>.scriptproviders (スクリプト プロバイダーの一覧表示)


**.Scriptproviders**コマンドには、アクティブ スクリプトのプロバイダーが一覧表示されます。

```dbgcmd
.scriptproviders 
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

.Scriptproviders コマンドには、デバッガーとする登録されている拡張機能によって現在認識されているすべてのスクリプト言語が一覧表示します。 終わるすべてのファイル"です。NatVis"は、NatVis スクリプトと考えるし、".js"で終わるすべてのファイルが JavaScript スクリプトとして認識します。 .Scriptload コマンドを使用してスクリプトのいずれかの型を読み込むことができます。

次の例では、JavaScript と NatVis プロバイダーが読み込まれます。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

**必要条件**

.Script コマンドのいずれかを使用するのには、スクリプトのプロバイダーが読み込まれる必要があります。 使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[**.scriptload (スクリプトの読み込み)**](-scriptload--load-script-.md)

 

 






