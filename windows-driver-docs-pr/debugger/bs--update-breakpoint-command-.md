---
title: bs (更新プログラムはブレークポイント コマンド)
description: Bs コマンドでは、指定したブレークポイントが発生した場合に実行されるコマンドを変更します。
ms.assetid: 624c9a30-a0d8-49bd-aba6-a46250022677
keywords:
- bs (更新プログラムはブレークポイント コマンド) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bs (Update Breakpoint Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 093a1550ed7c30ead4f7714ccef515dd38c06a90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559924"
---
# <a name="bs-update-breakpoint-command"></a>bs (更新プログラムはブレークポイント コマンド)


**Bs**コマンドは、指定したブレークポイントが発生した場合に実行されるコマンドを変更します。

```dbgcmd
bs ID ["CommandString"] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
ブレークポイントの ID 番号を指定します。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
新しいブレークポイントが検出されるたびに実行されるコマンドの一覧を指定します。 囲む必要があります、*クラスヒント*パラメーターを引用符で囲んで指定します。 セミコロンを使用して、複数のコマンドを区切ります。

デバッガーでのコマンド*クラスヒント*パラメーターを含めることができます。 標準 C コントロール文字を使用することができます (など **\\n**と **\\"**)。 引用符を 2 番目のレベルに格納されているセミコロン (**\\"**) 文字列を引用符で囲まれた、埋め込みの一部として解釈されます。

*クラスヒント*への応答、アプリケーションの実行中にブレークポイントに達した場合にのみコマンドが実行される、 **g (移動)** コマンド。 コードのステップまたはこのポイント以降をトレースする場合は、コマンドは実行されません。

いずれかのプログラムのブレークポイントの後の実行を再開コマンド (など**g**または**t**) コマンドの一覧の実行を終了します。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細とブレークポイント、他のブレークポイント コマンドや、ブレークポイントを制御する方法を使用する方法と、カーネル デバッガーからのユーザー領域でブレークポイントを設定する方法の例については、[を使用してブレークポイント](using-breakpoints.md)を参照してください。 条件付きブレークポイントの詳細については、[、条件付きブレークポイント](setting-a-conditional-breakpoint.md)を参照してください。

<a name="remarks"></a>注釈
-------

場合、*クラスヒント*が指定されていない、任意のコマンド ブレークポイントの設定が削除されます。

 

 





