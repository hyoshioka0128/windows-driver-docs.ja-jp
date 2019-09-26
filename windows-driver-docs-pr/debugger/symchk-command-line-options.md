---
title: SymChk のコマンドライン オプション
description: SymChk では、次の構文を使用します。
ms.assetid: e17dd001-2830-49bd-b727-fcd772ee23b4
keywords:
- SymChk コマンドラインオプションの Windows デバッグ
ms.date: 03/13/2019
topic_type:
- apiref
api_name:
- SymChk Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4efab9205ad19e717aa42d2f2b73adebc1f95d51
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284883"
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

## <a name="span-idddk_symchk_command_line_options_dtoolqspanspan-idddk_symchk_command_line_options_dtoolqspanparameters"></a><span id="ddk_symchk_command_line_options_dtoolq"></span><span id="DDK_SYMCHK_COMMAND_LINE_OPTIONS_DTOOLQ"></span>パラメータ


<span id="________r______"></span><span id="________R______"></span> **/r**   
*ファイル*でディレクトリが指定されている場合、 **/r**オプションを指定すると、symchk はこのディレクトリの下にあるすべてのサブディレクトリのプログラムファイルを再帰的に検索します。

<span id="________v______"></span><span id="________V______"></span> **/v**   
詳細情報を表示します。 これには、シンボルが調査されたすべてのプログラムファイルのファイル名と、そのパスに合格したか、失敗したか、または無視されたかが含まれます。

<span id="________q______"></span><span id="________Q______"></span> **/q**   
Quiet モードを有効にします。 すべての出力が抑制されます ( **/ot**オプションが含まれていない場合)。

<span id="_______FileNames______"></span><span id="_______filenames______"></span><span id="_______FILENAMES______"></span>*ファイル名*   
シンボルがチェックされるプログラムファイルを指定します。 絶対パス、相対パス、および UNC パスを使用できます。 アスタリスク ( **\*** ) ワイルドカードを使用できます。 \* ファイル名</em>の末尾にスラッシュが付いている場合は、ディレクトリ名として使用され、そのディレクトリ内のすべてのファイルがチェックされます。 *ファイル名*にスペースが含まれている場合は、引用符で囲む必要があります。

<span id="________ie_______ExeFile______"></span><span id="________ie_______exefile______"></span><span id="________IE_______EXEFILE______"></span> **/ie***Exefile*   
現在実行中のプログラムの名前を指定します。 このプログラムのシンボルがチェックされます。 *Exefile*には、ファイル拡張子とファイル拡張子 (通常は .exe) の名前を含める必要がありますが、パス情報は含まれません。 同じ名前を持つ2つの異なる実行可能ファイルがある場合、このオプションは推奨されません。 *Exefile*には、カーネルモードドライバーを含む任意のプログラムを指定できます。 *Exefile*が1つのアスタリスク ( **\*** ) の場合、symchk は、実行中のすべてのプロセス (ドライバーを含む) のシンボルをチェックします。

<span id="________id_______DumpFile______"></span><span id="________id_______dumpfile______"></span><span id="________ID_______DUMPFILE______"></span> **/id***ダンプファイル*   
メモリダンプファイルを指定します。 このダンプファイルのシンボルがチェックされます。

<span id="________ih_______HotFixFile______"></span><span id="________ih_______hotfixfile______"></span><span id="________IH_______HOTFIXFILE______"></span> **/ih***HotFixFile*   
自己解凍形式の修正プログラム CAB ファイルを指定します。

<span id="________ip_______ProcessID______"></span><span id="________ip_______processid______"></span><span id="________IP_______PROCESSID______"></span> **/ip***ProcessID*   
現在実行中のプログラムのプロセス ID を指定します。 このプログラムのシンボルがチェックされます。 *ProcessID*は10進数として指定する必要があります。 次の2つの特殊なワイルドカードがサポートされています。

- *ProcessID*がゼロ ( **0** ) の場合、symchk は実行中のすべてのドライバーのシンボルをチェックします。

- *ProcessID*が1つのアスタリスク ( **\*** ) の場合、symchk は、実行中のすべてのプロセス (ドライバーを含む) のシンボルをチェックします。

<span id="________it_______TextFileList______"></span><span id="________it_______textfilelist______"></span><span id="________IT_______TEXTFILELIST______"></span> **/it***Textfilelist*   
プログラムファイルの一覧を含むテキストファイルを指定します。 これらのプログラムのシンボルがすべてチェックされます。 *Textfilelist*は、ファイルを1つだけ指定する必要があります (相対パス、絶対パス、または UNC パスで、ワイルドカードは使用できません)。空白が含まれている場合は、引用符で囲む必要があります。 このファイル内では、各行がプログラムファイル (相対パス、絶対パス、または UNC パス) を示し、アスタリスク **\*** のワイルドカード () が許可されています。 ただし、このワイルドカードを使用するすべての行は、相対パスを使用する必要があります。

このファイルの行にスペースが含まれている場合は、引用符で囲む必要があります。 このファイル内のセミコロンは、コメント文字です。セミコロンと行末のすべてが無視されます。

<span id="________im_______ManifestList______"></span><span id="________im_______manifestlist______"></span><span id="________IM_______MANIFESTLIST______"></span> **/im***Manifestlist*   
コマンドへの入力が、 **/om**パラメーターを使用して以前に作成されたマニフェストファイルであることを指定します。 マニフェストファイルには、シンボルを取得する対象のファイルに関する情報が含まれています。 マニフェストファイルの使用方法の詳細については、「 [SymChk でのマニフェストファイルの使用](using-a-manifest-file-with-symchk.md)」を参照してください。

<span id="________om_______Manifest______"></span><span id="________om_______manifest______"></span><span id="________OM_______MANIFEST______"></span> **/om***マニフェスト*   
マニフェストファイルを作成することを指定します。 マニフェストファイルには、後で **/im**パラメーターを使用して、シンボルを取得する一連のファイルに関する情報が含まれています。

<span id="________s_Opts__SymbolPath"></span><span id="________s_opts__symbolpath"></span><span id="________S_OPTS__SYMBOLPATH"></span> **/s**パスの*パス*(i) \[\]  
シンボルを含むディレクトリを指定します。 絶対パス、相対パス、および UNC パスを使用できます。 任意の数のディレクトリを指定できます。複数のディレクトリをセミコロンで区切る必要があります。 *シンボルパス*にスペースが含まれている場合は、引用符で囲む必要があります。 このパス内にシンボルサーバーを指定する場合は、次のいずれかの構文を使用する必要があります。

```dbgcmd
srv*DownstreamStore*\\Server\Share
srv*\\Server\Share
```

**/S**\[のシンボルパスパラメーターは省略しないことをお勧めしますが、省略した場合、symchk は次の既定のパスを使用してパブリックシンボルストアをポイントします。\]

```dbgcmd
srv*%SystemRoot%\symbols*https://msdl.microsoft.com/download/symbols
```

次のオプションは、いずれも **/s**に従うことができます。 **/S**とこれらのオプションの間にスペースを配置することはできません。

<span id="e"></span><span id="E"></span>**つまり**  
SymChk は、すべてのパスを一度に確認するのではなく、各パスを個別にチェックします。

<span id="u"></span><span id="U"></span>**u**  
ダウンストリームストアが更新されます。 シンボルパスにダウンストリームストアが含まれている場合は、シンボルストアによってシンボルファイルが検索されます。 SymChk によって確認されているシンボルストアだけが更新されます。

<span id="p"></span><span id="P"></span>**irtran-p**  
プライベートシンボルを強制的にチェックします。 パブリックシンボルは一致しないものとして扱われます。 **P**オプションは**e**と**u**を意味し、 **s**と共に使用することはできません。

<span id="s"></span><span id="S"></span>**2$s**  
パブリック (分割) シンボルを強制的にチェックします。 プライベートシンボルは一致しないものとして扱われます。 **S**オプションは**e**と**u**を意味し、 **p**では使用できません。

<span id="r"></span><span id="R"></span> **\r\n\r\n**  
パスの詳細検索を実行するために、指定したパス内のすべての非シンボルサーバー要素を展開します。 注: このオプションは、指定されたシンボルパスを変更するため、デバッガー内では発生しない一致を生成する場合があります。


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
使用可能なオプションは、いくつかのクラスに分かれています。 オプションの各クラスは、さまざまな機能のセットを制御します。

**出力オプション。** 次のオプションの任意の数を指定できます。 これらのオプションは、 **/o**を使用した場合にのみ省略できます。たとえば、 **/oi/oe**は **/oie**として書き込むことができます。

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
<td align="left"><p>出力には個々のエラーが含まれます。 このオプションは、quiet モードがアクティブ化されていない場合に個別のエラーが自動的に表示されるため、 <strong>/q</strong>を使用する場合にのみ有効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/op</strong></p></td>
<td align="left"><p>出力には、によって渡される各ファイルが一覧表示されます。 (既定では、SymChk には、テストに失敗したファイルのみが表示されます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/oi</strong></p></td>
<td align="left"><p>出力には無視された各ファイルが一覧表示されます。 (既定では、SymChk には、テストに失敗したファイルのみが表示されます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/od</strong></p></td>
<td align="left"><p>出力には完全な詳細が含まれます。 <strong>/Oe/op/oi</strong>と同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ot</strong></p></td>
<td align="left"><p>出力には結果の合計が含まれます。 このオプションは、quiet モードがアクティブ化されていない場合に、これらの合計が自動的に表示されるため、 <strong>/q</strong>が使用されている場合にのみ役立ちます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ob</strong></p></td>
<td align="left"><p>バイナリの完全なパスは、すべての出力メッセージに含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/os</strong></p></td>
<td align="left"><p>シンボルの完全パスは、すべての出力メッセージに含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/oc</strong><em>ディレクトリ</em></p></td>
<td align="left"><p>SymChk は、チェックされたすべてのシンボルファイルの一覧を含む従来のシンボルツリー<em>を directory ディレクトリ</em>に作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ov</strong></p></td>
<td align="left"><p>SymChk は、チェックされたバイナリのバージョン情報も出力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ol</strong><em>ファイル</em></p></td>
<td align="left"><p>標準出力に送信されるメッセージに加えて、シンボルチェックを通過するすべてのバイナリとそのシンボルのコンマ区切りの一覧を含むファイルを作成します。</p></td>
</tr>
</tbody>
</table>

 

**DBG ファイルのオプション。** これらのオプションは、SymChk が dbg シンボルファイルをチェックする方法を制御し*ます*。 次のオプションのうち1つだけを指定できます。

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
<td align="left"><p>SymChk は、dbg 情報が実行可能ファイルから削除されたことを確認し、dbg ファイルにのみ表示され、実行可能ファイルが dbg ファイルを指していることを確認します。 プログラムが dbg シンボルファイルなしでビルドされた場合、このオプションによる影響はありません。 既定値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/de</strong></p></td>
<td align="left"><p>SymChk は、dbg 情報が実行可能ファイルから削除されていないこと、および実行可能ファイルが dbg ファイルを指していないことを確認します。 プログラムが dbg シンボルファイルなしでビルドされた場合、このオプションによる影響はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/dn</strong></p></td>
<td align="left"><p>SymChk は、dbg 情報がイメージに存在せず、イメージが dbg ファイルを指していないことを確認します。</p></td>
</tr>
</tbody>
</table>

 

**PDB ファイルのオプション。** これらのオプションは、SymChk が .pdb シンボルファイルをチェックする方法を制御します。 次のオプションのうち1つだけを指定できます。

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
<td align="left"><p>SymChk は .pdb ファイルの内容をチェックしません。ファイルが存在し、バイナリに一致することを確認するだけです。 既定値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ps</strong></p></td>
<td align="left"><p>SymChk は、ソース行、データ型、およびグローバル情報の .pdb ファイルが削除されたことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/pt</strong></p></td>
<td align="left"><p>SymChk は、.pdb ファイルにデータ型の情報が含まれていることを確認します。</p></td>
</tr>
</tbody>
</table>

 

**フィルターオプション。** これらのオプションは、SymChk がプロセスのチェックやファイルのダンプを行うときに、モジュールのフィルター処理を実行する方法を制御します。 次のオプションのうち1つだけを指定できます。

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
<td align="left"><p><strong>/fm</strong><em>モジュール</em></p></td>
<td align="left"><p>SymChk は、指定されたモジュールに関連付けられているダンプファイルまたはプロセスのみをチェックします。 <em>モジュール</em>には完全なファイル名を含める必要がありますが、ディレクトリパスの一部を含めることはできません。</p></td>
</tr>
</tbody>
</table>

 

**シンボルチェックオプション。** 次のオプションの任意の数を指定できます。

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
<td align="left"><p>SymChk は、CodeView データが存在するかどうかを検証しません。 (既定では、CodeView データの存在が確認されます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/cc</strong></p></td>
<td align="left"><p>SymChk が修正プログラムの CAB ファイルをチェックしている場合、cab 内のシンボルは検索されません。 (既定では、SymChk は、指定されたシンボルパスだけでなく、cab でもシンボルを検索します)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ea</strong><em>ファイル</em></p></td>
<td align="left"><p>SymChk は、指定したファイルに一覧表示されているプログラムのシンボルを検証しません。 これにより、特定のプログラムが検証されないように拒否することができます。 <em>ファイル</em>は、ファイルを1つだけ指定する必要があります (相対パス、絶対パス、または UNC パスで、ワイルドカードは使用できません)。空白が含まれている場合は、引用符で囲む必要があります。 <em>ファイル</em>内では、各行は、相対パス、絶対パス、または UNC パスによってプログラムファイルを示します。ワイルドカードは使用できません。 このファイル内の行にスペースが含まれている場合は、引用符で囲む必要があります。 このファイル内のセミコロンは、コメント文字です。セミコロンと行末のすべてが無視されます。 シンボルサーバーが使用されている場合、これらのプログラムのシンボルは下流ストアにコピーされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ee</strong><em>ファイル</em></p></td>
<td align="left"><p>指定したファイルに記載されているプログラムのエラーメッセージは表示されません。 "Success" メッセージと "ignore" メッセージは通常どおり表示され、シンボルファイルは通常どおり下流ストアにコピーされます。 <em>ファイル</em>の形式とその内容の形式は、 <strong>/ea</strong> <em>ファイル</em>の形式と同じです。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

SymChk の詳細については、「 [SymChk の使用](using-symchk.md)」を参照してください。

 

 





