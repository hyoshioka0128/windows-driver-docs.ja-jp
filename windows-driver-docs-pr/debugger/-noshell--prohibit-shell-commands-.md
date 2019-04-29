---
title: .noshell (シェル コマンドの禁止)
description: .Noshell コマンドから .shell コマンドを使用できません。
ms.assetid: 49a83e46-1390-4b60-bd61-a5da80c513e3
keywords:
- .noshell (シェルのコマンドを禁止する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .noshell (Prohibit Shell Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f51d8dd0333b8630456aa45fc3cb2e2bf05cc75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335897"
---
# <a name="noshell-prohibit-shell-commands"></a>.noshell (シェル コマンドの禁止)


**.Noshell**コマンドと使用できない[ **.shell** ](-shell--command-shell-.md)コマンド。

```dbgcmd
.noshell 
```

## <span id="ddk_meta_prohibit_shell_commands_dbg"></span><span id="DDK_META_PROHIBIT_SHELL_COMMANDS_DBG"></span>


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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

コマンド シェルの詳細については、および他のシェル コマンドを無効にする方法については、「[シェル コマンドを使用して](using-shell-commands.md)します。

<a name="remarks"></a>注釈
-------

使用する場合、 **.noshell**コマンドを使用することはできません[ **.shell (コマンド シェル)** ](-shell--command-shell-.md)新しいデバッグ セッションを開始する場合でも、デバッガーが実行されている限りをコマンドします。

リモート デバッグを実行する場合、このコマンドは、セキュリティのために便利です。

 

 





