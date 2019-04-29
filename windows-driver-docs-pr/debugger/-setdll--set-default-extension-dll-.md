---
title: .setdll (既定の拡張機能 DLL の設定)
description: .Setdll コマンドは、デバッガーの既定の拡張 DLL を変更します。
ms.assetid: 9dc5cd9e-d4f2-4112-bf3d-f7061c786ddf
keywords:
- 既定の拡張機能の DLL (.setdll) コマンドを設定します。
- 拡張機能のコマンド (コマンド)、既定の拡張 DLL を設定 (.setdll) コマンド
- .setdll (セット既定拡張 DLL) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .setdll (Set Default Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 32db5bf0ee2da68d7d1f9d8e71c9c6850cf9c622
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339799"
---
# <a name="setdll-set-default-extension-dll"></a>.setdll (既定の拡張機能 DLL の設定)


**.Setdll**のコマンドは、デバッガーの既定の拡張 DLL を変更します。

```dbgcmd
.setdll DLLName 
!DLLName.setdll 
```

## <a name="span-idddkmetasetdefaultextensiondlldbgspanspan-idddkmetasetdefaultextensiondlldbgspanparameters"></a><span id="ddk_meta_set_default_extension_dll_dbg"></span><span id="DDK_META_SET_DEFAULT_EXTENSION_DLL_DBG"></span>パラメーター


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span> *DLLName*   
名前と拡張 DLL のパス。 DLL が読み込まれるときに、完全なパスが指定されている場合で指定する完全なここでも、必要があります。

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

読み込みの詳細については、アンロード、および拡張機能を制御するを参照してください[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。 拡張機能のコマンドを実行する方法の詳細については、次を参照してください。[デバッガー拡張機能コマンドの使用](using-debugger-extension-commands.md)します。

<a name="remarks"></a>注釈
-------

デバッガーでは、既定の拡張機能、デバッガーが開始されると、暗黙的に読み込まれる DLL を保持します。 これにより、ユーザーが、拡張 DLL をロードすることがなく、拡張機能のコマンドを指定できます。 このコマンドにより、変更のうち、DLL が既定の DLL として読み込まれます。

コマンドが発行されると、デバッガーを既定の拡張機能は最初を検索します。 一致が見つからない場合は、それらが読み込まれる順序でその他のすべての拡張機能が読み込まれた Dll が検索されます。

 

 





