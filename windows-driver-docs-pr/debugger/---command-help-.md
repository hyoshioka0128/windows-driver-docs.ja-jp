---
title: (コマンドのヘルプ)
description: 疑問符 () は、すべてのコマンドと演算子の一覧を表示します。疑問符 () を単独では、コマンドのヘルプを表示します。 注意してください。
ms.assetid: 89b61021-43a4-46b7-ae43-a52dd9d40948
keywords:
- (コマンドのヘルプ)Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Command Help)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 07a278df4be296d05d9e2cfa3be0fc1ab835d545
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334845"
---
# <a name="-command-help"></a>? (コマンドのヘルプ)


疑問符 () (**?**) 文字は、すべてのコマンドと演算子の一覧を表示します。

**注**  疑問符 () を単独では、コマンドのヘルプを表示します。 [ **? 式**](---evaluate-expression-.md)構文は、指定された式を評価します。

```dbgcmd
    ?
```

## <span id="ddk_cmd_command_help_dbg"></span><span id="DDK_CMD_COMMAND_HELP_DBG"></span>


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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

標準コマンドの詳細については、使用 **?** します。 メタ コマンドの詳細については、使用[ **.help**](-help--meta-command-help-.md)します。 拡張機能コマンドの詳細については、使用[ **! ヘルプ**](-help.md)します。

 

 





