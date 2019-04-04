---
title: bsc (更新プログラムの条件付きブレークポイント)
description: Bsc コマンドでは、発生または指定した条件付きブレークポイントが発生した場合に実行されるコマンドを変更、ブレークポイント契約条件を変更します。
ms.assetid: 4d491797-3ba2-4a63-a575-67df39484bcf
keywords:
- bsc (更新プログラムの条件付きブレークポイント) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bsc (Update Conditional Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a0fc70c55d4dbeb8e6e00e5836c80e1d98f6262
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554015"
---
# <a name="bsc-update-conditional-breakpoint"></a>bsc (更新プログラムの条件付きブレークポイント)


**Bsc**コマンドが発生したまたは指定した条件付きブレークポイントが発生した場合に実行されるコマンドの変更、ブレークポイント契約条件を変更します。

```dbgcmd
bsc ID Condition ["CommandString"] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
ブレークポイントの ID 番号を指定します。

<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *条件*   
ブレークポイントがトリガーする条件を指定します。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
新しいブレークポイントが検出されるたびに実行されるコマンドの一覧を指定します。 囲む必要があります、*クラスヒント*パラメーターを引用符で囲んで指定します。 セミコロンを使用して、複数のコマンドを区切ります。

デバッガーでのコマンド*クラスヒント*パラメーターを含めることができます。 標準 C コントロール文字を使用することができます (など **\\n**と **\\"**)。 引用符を 2 番目のレベルに格納されているセミコロン (**\\"**) 文字列を引用符で囲まれた、埋め込みの一部として解釈されます。

クラスヒント コマンドの実行に対する応答で、アプリケーションの実行中にブレークポイントに達した場合にのみ、 **g (移動)** コマンド。 コードのステップまたはこのポイント以降をトレースする場合は、コマンドは実行されません。

いずれかのプログラムのブレークポイントの後の実行を再開コマンド (など**g**または**t**) コマンドの一覧の実行を終了します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>M<strong></strong>のため</p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細とブレークポイント、他のブレークポイント コマンドや、ブレークポイントを制御する方法を使用する方法と、カーネル デバッガーからのユーザー領域でブレークポイントを設定する方法の例については、[を使用してブレークポイント](using-breakpoints.md)を参照してください。 条件付きブレークポイントの詳細については、[、条件付きブレークポイント](setting-a-conditional-breakpoint.md)を参照してください。

<a name="remarks"></a>注釈
-------

場合、*クラスヒント*が指定されていない、任意のコマンド ブレークポイントの設定が削除されます。

使用して同じ効果を実現できる、 [ **bs (更新プログラムはブレークポイント コマンド)** ](bs--update-breakpoint-command-.md)コマンドと、次の構文。

```dbgcmd
bs ID "j Condition 'CommandString'; 'gc'"
```

 

 





