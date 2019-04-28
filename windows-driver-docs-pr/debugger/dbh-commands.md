---
title: DBH コマンド
description: DBH コマンド
ms.assetid: 124e8be9-1b1a-4498-84a4-5dbb6b5b9026
keywords:
- DBH、コマンド
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6901252e447d6635428b41b42d48f50b6a9f7e59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376070"
---
# <a name="dbh-commands"></a>DBH コマンド


DBH コマンドラインからシンボルとシンボル ファイルを分析するのにさまざまなコマンドを使用することができます。

DBH オプションを制御して他の基本的なタスクを実行するコマンドを次の表に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>verbose</strong> [<strong>on</strong>|<strong>off</strong>]</p></td>
<td align="left"><p>詳細出力モードを有効または無効にします。 パラメーターなしでは、現在の詳細出力モード設定を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sympath</strong> [<em>Path</em>]</p></td>
<td align="left"><p>シンボルの検索パスを設定します。 パラメーターなしでは、現在のシンボル検索パスを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>symopt</strong> <em>オプション</em></p>
<p><strong>symopt +</strong><em>オプション</em></p>
<p><strong>symopt -</strong><em>オプション</em></p>
<p><strong>symopt</strong></p></td>
<td align="left"><p>シンボル オプションを設定します。 ない<strong>+</strong>または<strong>-</strong>の値<em>オプション</em>現在のシンボルのオプションが置き換えられます。 場合<strong>+</strong>または<strong>-</strong>を使用する<em>オプション</em>追加または削除するオプションを指定する前にスペースが必要があります、 <strong> +</strong>または<strong>-</strong>が、その後に領域がありません。 パラメーターなしでは、現在のシンボルのオプションが表示されます。 DBH が起動され、すべてのシンボルのオプションの既定値は 0x10C13 が。 使用可能なオプションの一覧は、次を参照してください。<a href="symbol-options.md" data-raw-source="[Setting Symbol Options](symbol-options.md)">シンボル オプションを設定</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>help</strong></p></td>
<td align="left"><p>DBH コマンドのヘルプを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>終了</strong></p></td>
<td align="left"><p>DBH プログラムを終了します。</p></td>
</tr>
</tbody>
</table>

 

次の表は、読み込み、アンロード、および対象のモジュールを再設定するコマンドを一覧表示します。 DBH がコマンドラインでプロセス ID を指定することによって開始された場合、これらのコマンドを使用できません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>読み込む</strong><em>ファイル</em></p></td>
<td align="left"><p>指定したモジュールを読み込みます。 <em>ファイル</em>パス、ファイル名、および実行可能ファイルまたはシンボル ファイルのいずれかのファイル名拡張子を指定する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>unload</strong></p></td>
<td align="left"><p>現在のモジュールをアンロードします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>基本</strong><em>アドレス</em></p></td>
<td align="left"><p>既定のベース アドレスを指定した値に設定します。 シンボルのすべてのアドレスはこのベース アドレスに対して相対的に決定されます。</p></td>
</tr>
</tbody>
</table>

 

次の表は、ファイルを検索して、ディレクトリ情報を表示するコマンドを一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>findexe</strong> <em>ファイルのパス</em></p></td>
<td align="left"><p>指定されたパスに指定された実行可能ファイルの検索を使用して、 <strong>FindExecutableImage</strong>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>finddbg</strong> <em>ファイルのパス</em></p></td>
<td align="left"><p>指定されたパスに指定された .dbg ファイルを検索します。 .Dbg 拡張子を含むは省略可能です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dir</strong> <em>ファイルのパス</em></p></td>
<td align="left"><p>指定したパス、またはこのパスの下の任意のサブディレクトリ内に指定されたファイルを検索を使用して、 <strong>EnumDirTree</strong>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srchtree</strong> <em>ファイル パス</em></p></td>
<td align="left"><p>指定したパス、またはこのパスの下の任意のサブディレクトリ内に指定されたファイルを検索を使用して、 <strong>SearchTreeForFile</strong>ルーチン。 このコマンドは、同じ<strong>dir</strong>パラメーターは元に戻すことを除いて、します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ffpath</strong> <em>ファイル</em></p></td>
<td align="left"><p>現在のシンボル パスで指定されたファイルを検索します。</p></td>
</tr>
</tbody>
</table>

 

次の表には、モジュールの一覧とコントロールの既定のモジュールを解析するコマンドが表示されます。 DBH プロンプトには、既定のモジュールとそのベース アドレスが表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>mod</strong> <em>アドレス</em></p></td>
<td align="left"><p>指定したベース アドレスを使用して、モジュールを既定のモジュールを変更します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>refresh</strong></p></td>
<td align="left"><p>モジュールの一覧を更新します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>omap</strong></p></td>
<td align="left"><p>モジュールの OMAP 構造が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>epmod</strong> <em>PID</em></p></td>
<td align="left"><p>指定されたプロセスに読み込まれたすべてのモジュールを列挙します。 <em>PID</em>目的のプロセスのプロセス ID を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>情報</strong></p></td>
<td align="left"><p>現在読み込まれているモジュールに関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>obj</strong> <em>Mask</em></p></td>
<td align="left"><p>指定したパターンに一致する既定のモジュールに関連付けられているすべてのオブジェクト ファイルを一覧表示します。 <em>マスク</em>のさまざまなワイルドカード文字や; 指定子を含めることができますを参照してください<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>詳細についてはします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>src</strong> <em>Mask</em></p></td>
<td align="left"><p>指定したパターンに一致する既定のモジュールに関連付けられているすべてのソース ファイルを一覧表示します。 <em>マスク</em>のさまざまなワイルドカード文字や; 指定子を含めることができますを参照してください<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>詳細についてはします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enummod</strong></p></td>
<td align="left"><p>すべての読み込まれたモジュールを列挙します。 常に少なくとも 1 つのモジュール DBH がターゲットせず実行されていない場合である場合が含まれていません。</p></td>
</tr>
</tbody>
</table>

 

次の表では、コマンドを表示し、シンボルの検索を一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>列挙型</strong><em>モジュール</em><strong>!</strong><em>シンボル</em></p></td>
<td align="left"><p>指定したモジュールとシンボルに一致するすべてのシンボルを列挙します。 <em>モジュール</em>(ファイル名拡張子なし) を検索するモジュールを指定します。 <em>シンボル</em>シンボルを含める必要があるパターンを指定します。 両方<em>モジュール</em>と<em>シンボル</em>のさまざまなワイルドカード文字や; 指定子を含めることができますを参照してください<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>詳細についてはします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enumaddr</strong> <em>Address</em></p></td>
<td align="left"><p>指定したアドレスに関連付けられているすべてのシンボルを列挙します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>addr</strong> <em>Address</em></p></td>
<td align="left"><p>詳細については、指定したアドレスに関連付けられているシンボルを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>名前</strong>[<em>モジュール</em><strong>!</strong>]<em>シンボル</em></p></td>
<td align="left"><p>詳細については、指定されたシンボルを表示します。 省略可能な<em>モジュール</em>指定子を含めることができます。 ワイルドカードがないため、使用、パターンに一致する複数のシンボル場合<strong>名前</strong>のみその最初が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>[次へ]</strong> [<em>モジュール</em><strong>!</strong>]<em>シンボル</em></p>
<p><strong>[次へ]</strong> <em>アドレス</em></p></td>
<td align="left"><p>指定されたシンボルまたはアドレスの後の次の記号についての詳細を表示します。 シンボルが省略可能な名前で指定されたかどうか<em>モジュール</em>指定子を含めることができますが、ワイルドカードを使用する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>prev</strong> [<em>モジュール</em><strong>!</strong>]<em>シンボル</em></p>
<p><strong>prev</strong> <em>アドレス</em></p></td>
<td align="left"><p>詳細については、指定されたシンボルまたはアドレスより前の最初のシンボルを表示します。 シンボルが省略可能な名前で指定されたかどうか<em>モジュール</em>指定子を含めることができますが、ワイルドカードを使用する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>line</strong> <em>File</em><strong>#</strong><em>LineNum</em></p></td>
<td align="left"><p>指定したソースの行に関連付けられているバイナリ命令およびこの行に関連付けられている任意の記号の 16 進数のアドレスが表示されます。 指定した行の数と等しく、現在の行番号も設定します。 <em>ファイル</em>、ソース ファイルの名前を指定と<em>LineNum</em>はそのファイル内の行番号を指定します。 これらは、番号記号で区切る必要があります ( <strong> #</strong> )。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srclines</strong> <em>File LineNum</em></p></td>
<td align="left"><p>指定したソース行と行に関連付けられているバイナリの命令の 16 進数のアドレスに関連付けられているオブジェクト ファイルを表示します。 現在の行番号は変更されません。 <em>ファイル</em>、ソース ファイルの名前を指定と<em>LineNum</em>はそのファイル内の行番号を指定します。 これらは、スペースで区切る必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>laddr</strong> <em>アドレス</em></p></td>
<td align="left"><p>指定したアドレスにあるシンボルに対応するソース ファイルと行番号を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>linenext</strong></p></td>
<td align="left"><p>現在の行番号をインクリメントし、新しい行の数に関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lineprev</strong></p></td>
<td align="left"><p>デクリメント、現在の行番号と行番号を新しい情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>locals</strong> <em>Function</em> [<em>Mask</em>]</p></td>
<td align="left"><p>指定された関数内に含まれるすべてのローカル変数を表示します。 場合<em>マスク</em>に含まれている、指定したパターンに一致するローカルのみが表示されます。 を参照してください<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>詳細についてはします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>type</strong> <em>TypeName</em></p></td>
<td align="left"><p>指定したデータ型に関する詳細情報を表示します。 <em>TypeName</em>データ型 (たとえば、WSTRING) の名前を指定します。 この値に一致する型名がない場合は、一致するシンボルが表示されます。 ほとんどの DBH コマンド パラメーターとは異なり<em>TypeName</em>小文字が区別されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>elines</strong> [<em>ソース</em>[<em>Obj</em>]</p></td>
<td align="left"><p>指定したソース マスクとオブジェクトのマスクに一致するすべてのソース行を列挙します。 <em>ソース</em>絶対パスとファイル名拡張子を含むソース ファイルの名前を指定します。 <em>Obj</em>相対パスとファイル名拡張子を含む、オブジェクト ファイルの名前を指定します。 両方<em>ソース</em>と<em>Obj</em>のさまざまなワイルドカード文字や; 指定子を含めることができますを参照してください<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>詳細についてはします。 パラメーターを省略した場合、アスタリスクを使用することになります (<strong><em></strong>) ワイルドカードです。 パス情報を指定しない場合、ファイル名をプレフィックス<strong> </em> &lt;/strong&gt;をワイルドカード パスを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>index</strong> <em>Value</em></p></td>
<td align="left"><p>詳細については、指定したインデックス値のシンボルを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>スコープ</strong><em>アドレス</em></p>
<p><strong>スコープ</strong>[<em>モジュール</em><strong>!</strong>]<em>シンボル</em></p></td>
<td align="left"><p>詳細については、指定されたシンボルの親を表示します。 アドレスまたは名前は、シンボルを指定することがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srch</strong> [<strong>mask=</strong><em>Symbol</em>] [<strong>index=</strong><em>Index</em>] [<strong>tag=</strong><em>Tag</em>] [<strong>addr=</strong><em>Address</em>] [<strong>globals</strong>]</p></td>
<td align="left"><p>指定されたマスクに一致するすべてのシンボルを検索します。 <em>シンボル</em>シンボル名を指定します。 モジュール名を含める必要がありますいないが、ワイルドカード文字と指定子が含まれます参照してください<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>詳細についてはします。 <em>インデックス</em>検索の親として使用するシンボルの 16 進数のアドレスを指定します。 <em>タグ</em>16 進数の記号の種類の分類子を指定します (<strong>SymTag</strong><em>Xxx</em>) 記号に一致する必要がありますの値。 <em>アドレス</em>記号のアドレスを指定します。 場合<strong>globals</strong>が含まれている場合、グローバル シンボルのみが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uw</strong> <em>アドレス</em></p></td>
<td align="left"><p>指定したアドレスに、関数のアンワインド情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dtag</strong></p></td>
<td align="left"><p>すべてのシンボルの種類の分類子が表示されます (<strong>SymTag</strong><em>Xxx</em>) 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>etypes</strong></p></td>
<td align="left"><p>すべてのデータ型を列挙します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ダンプ</strong></p></td>
<td align="left"><p>ターゲット ファイルには、すべてのシンボル情報の完全な一覧を表示します。</p></td>
</tr>
</tbody>
</table>

 

次の表には、シンボル サーバーとシンボル ストアに関連するコマンドが表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>home</strong> [<em>Path</em>]</p></td>
<td align="left"><p>既定のダウン ストリーム ストア SymSrv と SrcSrv で使用される、ホーム ディレクトリを設定します。 シンボル パスには、既定のダウン ストリーム ストアを使用するシンボル サーバーへの参照が含まれている場合、 <strong>sym</strong>ホーム ディレクトリのサブディレクトリをダウン ストリームのストアに使用されます。 パラメーターなしで<strong>ホーム</strong>現在のホーム ディレクトリが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srvpath</strong> <em>パス</em></p></td>
<td align="left"><p>指定されたパスがシンボル ストアのパスであるかどうかをテストします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srvind</strong> <em>ファイル</em></p></td>
<td align="left"><p>指定したファイルに対応するシンボル サーバーのインデックスを検索します。 シンボル サーバーのインデックスは、かどうか実際に追加された任意のシンボル ストアに関係なく、ファイルの内容に基づく一意の値です。 <em>ファイル</em>目的のファイルの絶対パスとファイル名を指定する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>fii</strong> <em>ファイル</em></p></td>
<td align="left"><p>指定されたバイナリ ファイルとその関連ファイルのシンボル サーバーのインデックスが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>getfile</strong> <em>ファイルのインデックス</em></p></td>
<td align="left"><p>指定した名前とシンボル サーバーのインデックスを持つファイルを表示します。 <em>ファイル</em>目的のファイルの名前を指定します。 これは、パスは含まれません。 <em>インデックス</em>目的のファイルのシンボル サーバーのインデックスを指定します。 DBH を使用して、 <strong>SymFindFileInPath</strong>ルーチンをこの名前と、このインデックスを持つファイルの現在のシンボル パスの下のツリーを検索します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sup</strong> <em>File1 File2 のパス</em></p></td>
<td align="left"><p>パラメーターの値に基づいて、シンボル ストアにファイルを格納します。 <em>パス</em>シンボル ストアのディレクトリ パスを指定します。 <em>File1</em>と<em>File2</em>順番に格納されているファイルを識別するために使用される差分値を作成するために使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>storeadd</strong> <em>ファイル ストア</em></p></td>
<td align="left"><p>指定されたシンボル ストアには、指定したファイルを追加します。 <em>格納</em>シンボル ストアのルート パスを指定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

次の表には、実数部と虚数部のシンボルに適用される DBH コマンドが表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>undec</strong> <em>Name</em></p></td>
<td align="left"><p>指定されたシンボル名に接続されている文字装飾の意味がわかります。 <em>名前</em>任意の文字列を使用することができます。 その必要がある、現在読み込まれているシンボルに対応していません。 場合<em>名前</em>C++ の装飾が含まれています。 これらの装飾の意味が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>追加</strong><em>名アドレス サイズ</em></p></td>
<td align="left"><p>DBH に読み込まれたシンボルの一覧には、指定の虚数部のシンボルを追加します。 <em>名前</em>追加するには、シンボルの名前を指定<em>アドレス</em>の 16 進数のアドレスを指定します、<em>サイズ</em>の 16 進数のサイズ (バイト単位)。 DBH セッションが終了するまでその他の記号の後の DBH コマンドのように扱われますこの<strong>終了</strong>または<strong>アンロード</strong>と虚数部のシンボルが削除されるまで、または<strong>del</strong>します。実際のターゲットのシンボル ファイルは変更されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>del</strong> <em>名</em></p>
<p><strong>del</strong> <em>アドレス</em></p></td>
<td align="left"><p>先ほど追加したと虚数部のシンボルを削除、<strong>追加</strong>コマンド。 シンボルは、名前またはアドレスのいずれかに指定できます。 これは、実際のシンボルの削除を使用できません。</p></td>
</tr>
</tbody>
</table>

 

 

 





