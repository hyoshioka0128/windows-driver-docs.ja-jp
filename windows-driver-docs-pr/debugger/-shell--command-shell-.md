---
title: .shell (コマンド シェル)
description: .Shell コマンドでは、シェル プロセスを起動し、デバッガーにまたは指定したファイルには、その出力をリダイレクトします。
ms.assetid: 351cbd54-6e1a-4dc1-b0d8-8e61294b0e86
keywords:
- コマンド シェル (.shell) コマンド
- MS-DOS シェル (.shell) コマンド
- DOS シェル (.shell) コマンド
- シェル コマンド、コマンド シェル (.shell) コマンド
- .shell (コマンド シェル) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .shell (Command Shell)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24774ef64bb31b80eb473bee91ccf4b35cfb5068
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550721"
---
# <a name="shell-command-shell"></a>.shell (コマンド シェル)


**.Shell**コマンド シェル プロセスを起動し、デバッガーにまたは指定したファイルには、その出力をリダイレクトします。

```dbgcmd
.shell [Options] [ShellCommand] 
.shell -i InFile [-o OutFile [-e ErrFile]] [Options] ShellCommand
```

## <a name="span-idddkmetacommandshelldbgspanspan-idddkmetacommandshelldbgspanparameters"></a><span id="ddk_meta_command_shell_dbg"></span><span id="DDK_META_COMMAND_SHELL_DBG"></span>パラメーター


<span id="_______InFile______"></span><span id="_______infile______"></span><span id="_______INFILE______"></span> *InFile*   
入力に使用するファイルのパスとファイル名を指定します。 代わりに 1 つのハイフン (-) を指定するには最初のコマンドの後に入力が提供されない場合は、 *InFile*ハイフンの前にスペースを入れずにします。

<span id="_______OutFile______"></span><span id="_______outfile______"></span><span id="_______OUTFILE______"></span> *出力ファイルします。*   
標準出力に使用するファイルのパスとファイル名を指定します。 場合 **-o** **** *OutFile*は省略すると、出力は、デバッガー コマンド ウィンドウに送信されます。 この出力を表示するか、ファイルに保存したくない場合は、代わりに 1 つのハイフン (-) を指定できます*OutFile*ハイフンの前にスペースを入れずにします。

<span id="_______ErrFile______"></span><span id="_______errfile______"></span><span id="_______ERRFILE______"></span> *最大*   
エラー出力に使用するファイルのパスとファイル名を指定します。 -E 最大を省略した場合は、エラー出力が標準出力と同じ場所に送信されます。 この出力を表示するか、ファイルに保存したくない場合は、代わりに 1 つのハイフン (-) を指定できます*最大*ハイフンの前にスペースを入れずにします。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の数を指定できます。

<span id="-ci__Commands_"></span><span id="-ci__commands_"></span><span id="-CI__COMMANDS_"></span>**-ci"**<em>コマンド</em>**"**  
指定されたデバッガーのコマンドを処理し、入力ファイルとして起動されるプロセスにその出力を渡します。 *コマンド*のデバッガー コマンドでは、任意の数が、セミコロンで区切られたし、引用符で囲まれたすることができます。

<span id="-x"></span><span id="-X"></span>**-x**  
デバッガーから完全にデタッチするために生成されている任意のプロセスをによりします。 でも実行を続行するプロセスを作成できます、デバッグ セッションの後に終了します。

<span id="_______ShellCommand______"></span><span id="_______shellcommand______"></span><span id="_______SHELLCOMMAND______"></span> *ShellCommand*   
Microsoft MS-DOS のコマンドを実行するアプリケーションのコマンドラインを指定します。

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

コマンド シェルにアクセスするその他の方法では、[シェル コマンドを使用して](using-shell-commands.md)を参照してください。

<a name="remarks"></a>注釈
-------

**.Shell**カーネル デバッガーに、ユーザー モード デバッガーの出力がリダイレクトされたときに、コマンドがサポートされていません。 カーネル デバッガー (KD 経由では NTSD と呼ばれることもあります) への出力のリダイレクトの詳細については、[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)を参照してください。

全体の行に、 **.shell** (セミコロンが含まれている) 場合でもにそのコマンドが Windows のコマンドとして解釈されます。 この行は、引用符で囲まれていない必要があります。 間にスペースがある **.shell**と*ShellCommand* (追加の先頭のスペースは無視されます)。

しない限り、デバッガー コマンド ウィンドウで、コマンドの出力が表示されます、 **-o** **** *OutFile*パラメーターを使用します。

発行、 **.shell**パラメーターなしでコマンド シェルをアクティブ化し、開いたままにします。 すべての後続のコマンドは、Windows のコマンドとして解釈されます。 この期間中、デバッガーが読み取るメッセージを表示 **&lt;.shell プロセスは、入力を必要があります&gt;** と WinDbg のプロンプトに置き換え、**入力&gt;** プロンプト。 場合によっては、別のコマンド プロンプト ウィンドウは、デバッガーが離れるシェルが開いているときに表示されます。 このウィンドウを無視する必要があります。すべての入力し、出力は、デバッガー コマンド ウィンドウから実行されます。

このシェルを閉じ、デバッガー自体に戻り、次のように入力します。**終了**または **.shell\_終了**します。 (、 **.Shell\_終了**コマンドは、シェルが固定されている場合でも動作するためにさらに強力です)。

このコマンドは、CSRSS にアクティブにせず、新しいプロセスを作成できないために、CSRSS、デバッグ中に使用できません。

1 つまたは複数のデバッガー コマンドを実行し、その出力をシェル プロセスに渡すには、-ci フラグを使用できます。 例からの出力を渡すことができます、 [ **! 0 7 の処理**](-process.md)コマンドを次のコマンドを使用して、Perl スクリプト。

```dbgcmd
0:000> .shell -ci "!process 0 7" perl.exe parsemyoutput.pl 
```

 

 





