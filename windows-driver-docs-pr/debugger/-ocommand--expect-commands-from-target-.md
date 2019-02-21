---
title: .ocommand (ターゲットからのコマンドを想定)
description: .Ocommand コマンドでは、デバッガーにコマンドを送信する対象のアプリケーションを使用します。
ms.assetid: a4363395-111f-48eb-b1da-c17c0ad9f067
keywords:
- コマンド ターゲット (.ocommand) コマンドに期待します。
- .ocommand (ターゲットからのコマンドを想定) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ocommand (Expect Commands from Target)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2fed3a43c22ade7994ff92ebd3df1bbf8a32b470
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552529"
---
# <a name="ocommand-expect-commands-from-target"></a>.ocommand (ターゲットからのコマンドを想定)


**.Ocommand**コマンドにより、対象のアプリケーション、デバッガーにコマンドを送信します。

```dbgcmd
.ocommand  String 
.ocommand -d 
.ocommand 
```

## <a name="span-idddkmetaexpectcommandsfromtargetdbgspanspan-idddkmetaexpectcommandsfromtargetdbgspanparameters"></a><span id="ddk_meta_expect_commands_from_target_dbg"></span><span id="DDK_META_EXPECT_COMMANDS_FROM_TARGET_DBG"></span>パラメーター


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *文字列*   
コマンドのプレフィックス文字列を指定します。 *文字列*、スペースを含めることができますなどの C スタイルの制御文字を使用できません **\\"** と **\\n**します。 囲むこともできます*文字列*引用符で囲んで指定します。 ただし場合、*文字列*セミコロン、スペースを先頭または末尾のスペースが含まれています囲む必要があります*文字列*引用符で囲んで指定します。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
コマンドのプレフィックス文字列を削除します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
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

詳細については[ **OutputDebugString** ](https://msdn.microsoft.com/library/windows/desktop/aa363362)と、デバッガーと通信するその他のユーザー モード関数は、Microsoft Windows SDK のマニュアルを参照してください。

<a name="remarks"></a>注釈
-------

使用する場合、 **.ocommand**パラメーターを指定せずコマンドと、デバッガーは、現在のコマンド プレフィックス文字列を表示します。 既存の文字列をクリアする **.ocommand-d**します。

すべてターゲットの出力をコマンドのプレフィックス文字列を設定したら、(の内容など、 [ **OutputDebugString** ](https://msdn.microsoft.com/library/windows/desktop/aa363362)コマンド) がスキャンされます。 この出力は、コマンドのプレフィックス文字列で始まっている場合、プレフィックス文字列を次の出力のテキストはデバッガー コマンド文字列として扱われを実行します。 このテキストが実行されたときにコマンド文字列は表示されません。

ターゲットを含めることができます、 [ **.echo (エコー コメント)** ](-echo--echo-comment-.md)メッセージを追加する場合、出力文字列にコマンドします。 プレフィックス文字列で始まらないターゲットの出力は、通常どおりに表示されます。

コマンド内のコマンドの後に文字列が実行されたら、最後のコマンドがない限り、デバッガーに分割、ターゲットは[ **g (移動)**](g--go-.md)します。

コマンドのプレフィックス文字列とターゲットの出力の比較では、大文字小文字を区別しません。 (ただし、後続の使用 **.ocommand**保持ケースで入力した文字列の表示)。

この例では、デバッガーでは、次のコマンドを入力することを想定しています。

```dbgcmd
0:000> .ocommand magiccommand
```

次に、対象アプリケーションは、次の行を実行します。

```dbgcmd
OutputDebugString("MagicCommand kb;g");
```

デバッガーは、コマンド文字列の先頭を認識し、実行**kb、g**すぐにします。

ただし、次の行では、任意のコマンドを実行するのには発生しません。

```dbgcmd
OutputDebugString("Command on next line.\nmagiccommand kb;g");
```

新しい行が始まっても、出力の先頭にコマンド文字列の先頭でないため、前の例から実行するコマンドはありません。

**注**  独自のコマンド以外に任意のターゲットの場合は表示されませんが、コマンド文字列プレフィックスは出力を選択する必要があります。

 

 

 





