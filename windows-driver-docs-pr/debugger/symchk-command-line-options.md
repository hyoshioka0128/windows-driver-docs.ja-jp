---
title: SymChk のコマンドライン オプション
description: SymChk は、次の構文を使用します。
ms.assetid: e17dd001-2830-49bd-b727-fcd772ee23b4
keywords:
- SymChk コマンド ライン オプションの Windows デバッグ
ms.date: 03/13/2019
topic_type:
- apiref
api_name:
- SymChk Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: af4639590b1e434e15273f978c192112d78096c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379740"
---
# <a name="symchk-command-line-options"></a>SymChk のコマンドライン オプション


SymChk では、次の構文を使用します。

```dbgcmd
symchk [/r] [/v | /q ] FileNames /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /ie ExeFile /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /id DumpFile /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /ih HotFixFile /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /ip ProcessID /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /it TextFileList /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /om Manifest FileNames

symchk [/v | /q ] /im ManifestList /s[Opts] SymbolPath Options

symchk [/v | /q ] /om Manifest /ie ExeFile

symchk [/v | /q ] /om Manifest /id DumpFile

symchk [/v | /q ] /om Manifest /ih HotFixFile

symchk [/v | /q ] /om Manifest /ip ProcessFile

symchk [/v | /q ] /om Manifest /it TextFileList
```

## <a name="span-idddksymchkcommandlineoptionsdtoolqspanspan-idddksymchkcommandlineoptionsdtoolqspanparameters"></a><span id="ddk_symchk_command_line_options_dtoolq"></span><span id="DDK_SYMCHK_COMMAND_LINE_OPTIONS_DTOOLQ"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
場合*ファイル*ディレクトリを指定します、 **/r**オプションにより SymChk を再帰的には、プログラム ファイルのこのディレクトリの下のすべてのサブディレクトリを検索します。

<span id="________v______"></span><span id="________V______"></span> **/v**   
詳細な情報を表示します。 これには、その記号を調査したすべてのプログラム ファイルのファイル名が含まれます、渡された、失敗、または無視されますが、かどうか。

<span id="________q______"></span><span id="________Q______"></span> **/q**   
Quiet モードを有効にします。 すべての出力が表示されなくなります (しない限り、 **/ot**オプションが含まれる)。

<span id="_______FileNames______"></span><span id="_______filenames______"></span><span id="_______FILENAMES______"></span> *FileNames*   
シンボルがチェックするには、プログラム ファイルを指定します。 絶対パス、相対パス、および UNC パスが許可されます。 アスタリスク (**\\**<em>) ワイルドカードが許可されます。場合 * ファイル名</em>実行ディレクトリ名を指定するのにはスラッシュで終了すると、およびそのディレクトリ内のすべてのファイルがチェックされます。 場合*ファイル名*スペースが含まれることは、引用符で囲む必要があります。

<span id="________ie_______ExeFile______"></span><span id="________ie_______exefile______"></span><span id="________IE_______EXEFILE______"></span> **/ie** *ExeFile*   
現在実行しているプログラムの名前を指定します。 このプログラムのシンボルがチェックされます。 *ExeFile*パス情報はありませんが、ファイルとファイル拡張子 (通常は .exe) の名前を含める必要があります。 2 つの異なる実行可能ファイルと同じ名前がある場合は、このオプションは推奨されません。 *ExeFile*カーネル モード ドライバーを含む、任意のプログラムを指定できます。 場合*ExeFile*は 1 つのアスタリスク ( **\\***)、SymChk はドライバーを含むすべての実行プロセスのシンボルを確認します。

<span id="________id_______DumpFile______"></span><span id="________id_______dumpfile______"></span><span id="________ID_______DUMPFILE______"></span> **/id** *ダンプ ファイル*   
メモリ ダンプ ファイルを指定します。 このダンプ ファイルのシンボルがチェックされます。

<span id="________ih_______HotFixFile______"></span><span id="________ih_______hotfixfile______"></span><span id="________IH_______HOTFIXFILE______"></span> **/ih** *HotFixFile*   
自己解凍形式の修正プログラムの CAB ファイルを指定します。

<span id="________ip_______ProcessID______"></span><span id="________ip_______processid______"></span><span id="________IP_______PROCESSID______"></span> **/ip** *ProcessID*   
現在実行しているプログラムのプロセス ID を指定します。 このプログラムのシンボルがチェックされます。 *ProcessID* 10 進数として指定する必要があります。 サポートされている 2 つの特殊なワイルドカードがあります。

- 場合*ProcessID*は 0 です ( **0** )、SymChk は実行中のすべてのドライバーのシンボルを確認します。

- 場合*ProcessID*は 1 つのアスタリスク ( **\\***)、SymChk はドライバーを含むすべての実行プロセスのシンボルを確認します。

<span id="________it_______TextFileList______"></span><span id="________it_______textfilelist______"></span><span id="________IT_______TEXTFILELIST______"></span> **/it** *TextFileList*   
プログラム ファイルの一覧を含むテキスト ファイルを指定します。 これらすべてのプログラムのシンボルがチェックされます。 *TextFileList*引用符で囲む必要がありますにスペースが含まれる場合、1 つのファイル (で相対パス、絶対パス、または UNC パスが、ワイルドカードなしで); を指定する必要があります。 このファイルでそれぞれの行を示します (相対パス、絶対パス、または UNC パス) をプログラム ファイルと、アスタリスクのワイルドカード (* *\\* * *) は許可されています。 ただし、このワイルドカードを使用して任意の行では、相対パスを使用する必要があります。

このファイル内の行にスペースが含まれている場合は、引用符で囲む必要があります。 このファイル内でセミコロンは、コメント文字です--すべてセミコロンと行の末尾の間は無視されます。

<span id="________im_______ManifestList______"></span><span id="________im_______manifestlist______"></span><span id="________IM_______MANIFESTLIST______"></span> **/im** *ManifestList*   
コマンドへの入力を使用して、以前に作成したマニフェスト ファイルに指定します、 **/om**パラメーター。 マニフェスト ファイルには、シンボルが取得されるファイルに関する情報が含まれています。 詳細についてはマニフェスト ファイルを使用して、次を参照してください。 [SymChk でマニフェスト ファイルの使用](using-a-manifest-file-with-symchk.md)します。

<span id="________om_______Manifest______"></span><span id="________om_______manifest______"></span><span id="________OM_______MANIFEST______"></span> **/om** *Manifest*   
マニフェスト ファイルが作成されたことを指定します。 マニフェスト ファイルにはシンボルが取得されを使用してファイルのセットに関する情報が含まれています、 **/im**は後でのパラメーター。

<span id="________s_Opts__SymbolPath"></span><span id="________s_opts__symbolpath"></span><span id="________S_OPTS__SYMBOLPATH"></span> **/s**\[*opts* \] *SymbolPath*  
シンボルを含むディレクトリを指定します。 絶対パス、相対パス、および UNC パスが許可されます。 ディレクトリの任意の数を指定することができます - 複数のディレクトリをセミコロンで区切る必要があります。 場合*SymbolPath*スペースが含まれることは、引用符で囲む必要があります。 をこのパス内のシンボル サーバーを指定する場合は、次の構文のいずれかを使用する必要があります。

```dbgcmd
srv*DownstreamStore*\\Server\Share
srv*\\Server\Share
```

省略することはお勧めできません、 **/s**\[*Opts* \] *SymbolPath* SymChk が場合は省略すると、パラメーターにポイントして、パブリック次の既定のパスを使用して、シンボル ストア:

```dbgcmd
srv*%SystemRoot%\symbols*https://msdl.microsoft.com/download/symbols
```

次のオプションの任意の数に従って **/s**します。 間にスペースが存在できるように、 **/s**とこれらのオプション。

<span id="e"></span><span id="E"></span>**E**  
SymChk では、一度にすべてのパスを確認する代わりに個別に各パスを確認します。

<span id="u"></span><span id="U"></span>**U**  
ダウン ストリームのストアが更新されます。 シンボル パスには、ダウン ストリームのストアが含まれている場合は、シンボル ファイルのシンボル ストアが検索されます。 SymChk によって検査されている唯一のシンボル ストアが更新されます。

<span id="p"></span><span id="P"></span>**P**  
プライベート シンボルのチェックを強制します。 パブリック シンボルは、一致しないとして扱われます。 **P**が暗黙的に指定**e**と**u**とでは使用できません**s**します。

<span id="s"></span><span id="S"></span>**s**  
パブリック (分割) 記号のチェックを強制します。 プライベート シンボルは、一致しないとして扱われます。 **S**が暗黙的に指定**e**と**u**とでは使用できません**p**します。

<span id="r"></span><span id="R"></span>**R**  
パスの詳細な検索を実行するには、指定されたパス内のすべての非シンボル サーバー要素を展開します。 注: このオプションには、指定されたシンボル パスが変更されますので、デバッガー内では行われません一致が発生します。


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
使用可能なオプションは、いくつかのクラスに分割されます。 オプションの各クラスは、異なる一連の機能を制御します。

**出力オプション。** 次のオプションの任意の数を指定することができます。 使用してこれらのオプションを省略できます **/o**例については、- のみ 1 回 **/oi/oe**として記述できます **/oie**します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/oe</strong></p></td>
<td align="left"><p>出力は、個々 のエラーが含まれます。 このオプションは場合<strong>/q</strong> quiet モードをアクティブ化されていない場合に、個々 のエラーが自動的に表示されるため、使用されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/op</strong></p></td>
<td align="left"><p>出力に渡される各ファイルが表示されます。 (既定では、SymChk のみが表示されますテストに失敗したファイルです。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/oi</strong></p></td>
<td align="left"><p>出力には、各無視されたファイルが表示されます。 (既定では、SymChk のみが表示されますテストに失敗したファイルです。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/od</strong></p></td>
<td align="left"><p>出力は、完全な詳細情報が含まれます。 同じ<strong>/oe/op/oi</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ot</strong></p></td>
<td align="left"><p>出力結果の合計が含まれます。 このオプションは場合<strong>/q</strong> quiet モードをアクティブ化されていない場合に、これらの合計が自動的に表示されるため、使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ob</strong></p></td>
<td align="left"><p>バイナリの完全なパスは、すべての出力メッセージに含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/os</strong></p></td>
<td align="left"><p>シンボルの完全なパスは、すべての出力メッセージに含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/oc</strong> <em>Dir</em></p></td>
<td align="left"><p>SymChk はディレクトリに従来のシンボルのツリーを作成<em>Dir</em>チェックされているすべてのシンボル ファイルの一覧を格納しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ov</strong></p></td>
<td align="left"><p>SymChk も確認済みのバイナリのバージョン情報が出力されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ol</strong> <em>ファイル</em></p></td>
<td align="left"><p>標準出力に送信されたメッセージ、だけでなく、コンマを含むファイルの書き込みには、すべてのバイナリおよびシンボルのチェックに合格した、シンボルの一覧が区切られます。</p></td>
</tr>
</tbody>
</table>

 

**DBG ファイルのオプションです。** これらのオプションが SymChk を確認する方法を制御 *.dbg*シンボル ファイル。 次のオプションの 1 つだけを指定することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/ds</strong></p></td>
<td align="left"><p>.Dbg ファイルを実行可能ファイルを指していると .dbg 情報は、実行可能ファイルから削除され、.dbg ファイルでのみ表示されます、SymChk を確認します。 .Dbg シンボル ファイルなしでビルドされたプログラムは場合、は、このオプションに影響はありません。 既定値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/de</strong></p></td>
<td align="left"><p>SymChk は .dbg 情報が、実行可能ファイルから取り除かれていないことと、実行可能ファイルは .dbg ファイルを指していないことを確認します。 .Dbg シンボル ファイルなしでビルドされたプログラムは場合、は、このオプションに影響はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/dn</strong></p></td>
<td align="left"><p>SymChk は .dbg 情報が、イメージに存在しないことと、イメージは .dbg ファイルを指していないことを確認します。</p></td>
</tr>
</tbody>
</table>

 

**PDB ファイルのオプションです。** これらのオプションは、SymChk が .pdb シンボル ファイルをチェックする方法を制御します。 次のオプションの 1 つだけを指定することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/pf</strong></p></td>
<td align="left"><p>SymChk の実行で .pdb ファイルの内容をチェックしない--ファイルが存在し、バイナリと一致したことを確認します。 既定値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ps</strong></p></td>
<td align="left"><p>SymChk はソース行、データ型、およびグローバル情報の .pdb ファイルが削除されたことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/pt</strong></p></td>
<td align="left"><p>SymChk は .pdb ファイルがデータ型情報を含むことを確認します。</p></td>
</tr>
</tbody>
</table>

 

**オプションのフィルター処理します。** これらのオプションは、モジュールがフィルター処理の実行方法のプロセスまたはダンプ ファイル SymChk がチェックするときに制御します。 次のオプションの 1 つだけを指定することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/fm</strong> <em>モジュール</em></p></td>
<td align="left"><p>SymChk はダンプ ファイル、または指定したモジュールに関連付けられたプロセスにのみ確認します。 <em>モジュール</em>完全なファイル名を含める必要がありますが、ディレクトリ パスの任意の部分を含めることはできません。</p></td>
</tr>
</tbody>
</table>

 

**シンボル オプションを確認します。** 次のオプションの任意の数を指定することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/cs</strong></p></td>
<td align="left"><p>SymChk は CodeView データが存在することを検証できません。 (既定では、CodeView データの存在は検証されます。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/cc</strong></p></td>
<td align="left"><p>SymChk では、修正プログラムの CAB ファイルを確認するとき、cab ファイル内のシンボルは検索しません。 (既定では、SymChk がシンボルを検索で指定されたシンボル パスのようにも cab。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ea</strong> <em>ファイル</em></p></td>
<td align="left"><p>SymChk には、指定したファイルに記載されているプログラムのシンボルを検証できません。 これにより、それ以外の場合はことを確認する特定のプログラムを拒否できます。 <em>ファイル</em>引用符で囲む必要がありますにスペースが含まれる場合、(で相対パス、絶対パス、または UNC パスが、ワイルドカードを含まない)。 1 つのファイルを指定する必要があります。 内で<em>ファイル</em>各行が (相対パス、絶対パス、または UNC パス) をプログラム ファイルを示します。 ワイルドカードは許可されません。 このファイル内の行にスペースが含まれている場合は、引用符で囲む必要があります。 このファイル内でセミコロンは、コメント文字です--すべてセミコロンと行の末尾の間は無視されます。 シンボル サーバーを使用している場合、これらのプログラムのシンボルはダウン ストリームのストアにコピーされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ee</strong> <em>ファイル</em></p></td>
<td align="left"><p>指定したファイルに表示されているこれらのプログラムのエラー メッセージが表示されません。 「成功」と「無視」メッセージが通常どおりに表示され、シンボル ファイルを通常どおり、ダウン ストリームのストアにコピーされます。 形式<em>ファイル</em>とその内容の形式がの場合と同じ<strong>/ea</strong> <em>ファイル</em>します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

SymChk の詳細については、次を参照してください。[を使用して SymChk](using-symchk.md)します。

 

 





