---
title: ユーザーモード ダンプ ファイル
description: ユーザーモード ダンプ ファイル
ms.assetid: bef29d75-6620-4219-b402-36fbddc4fe1f
keywords:
- ダンプ ファイル、ユーザー モード
ms.date: 08/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8c5e96f53806931cfc846ef7167e204a23dc6d12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367978"
---
# <a name="user-mode-dump-files"></a>ユーザーモード ダンプ ファイル

このセクションの内容:

- [さまざまなユーザー モードのダンプ ファイル](#varieties)

- [ユーザー モード ダンプ ファイルを作成します。](#creating)

ダンプ ファイルの分析方法の詳細については、次を参照してください。[ユーザー モード ダンプ ファイルの分析](analyzing-a-user-mode-dump-file.md)します。


## <a name="span-idvarietiesspanspan-idvarietiesspan-varieties-of-user-mode-dump-files"></a><span id="varieties"></span><span id="VARIETIES"></span> さまざまなユーザー モードのダンプ ファイル

ユーザー モード クラッシュ ダンプ ファイルのいくつかの種類がありますが、これらは、2 つのカテゴリに分類されます。

[完全なユーザー モード ダンプ](#full)

[ミニダンプ](#minidumps)

これらのダンプ ファイルの違いは、サイズのいずれかです。 ミニダンプは、通常よりコンパクトなアナリストに簡単に送信できます。

**注**  ダンプ ファイルを分析することで、多くの情報を取得できます。 ただし、ダンプ ファイルが提供できない情報をできるだけ実際には、デバッガーで直接、クラッシュをデバッグします。


## <a name="span-idfullspanspan-idfullspanfull-user-mode-dumps"></a><span id="full"></span><span id="FULL"></span>完全なユーザー モード ダンプ

A*フル ユーザー モード ダンプ*は、基本的なユーザー モード ダンプ ファイルです。

このダンプ ファイルには、プロセス、プログラムの実行可能イメージ自体、ハンドル テーブル、およびデバッガーに役に立つその他の情報のすべてのメモリ領域が含まれます。

ミニダンプにフル ユーザー モード ダンプ ファイルを「縮小」することになります。 単にダンプ ファイルをデバッガーに読み込むし、使用して、 [ **.dump (ダンプ ファイルの作成)** ](-dump--create-dump-file-.md)ミニダンプの形式で新しいダンプ ファイルを保存するコマンド。

**注**   、その名前に関係なく、最も大きな「ミニダンプ」ファイルには実際にが含まれています、フル ユーザー モード ダンプより多くの情報には。 たとえば、 **.dump/mf**または **.dump/ma**よりも大きいとより完全なファイルが作成されます **.dump/f**します。


ユーザー モードで **.dump/m\[**<em>MiniOptions</em> **\]** をお勧めします。 このスイッチを使用して作成されたダンプ ファイルは、非常に大規模なから非常に小さいサイズに変更できます。 適切なを指定することによって*MiniOptions*正確にどのような情報が含まれるかを制御できます。



## <a name="span-idminidumpsspanspan-idminidumpsspanminidumps"></a><span id="minidumps"></span><span id="MINIDUMPS"></span>ミニダンプ

プロセスに関連付けられているメモリの一部だけを含むユーザー モード ダンプ ファイルと呼ばれる、*ミニダンプ*します。

ミニダンプ ファイルの内容とサイズは、ダンプされるプログラムと、ダンプを行うアプリケーションによって異なります。 場合によっては、ミニダンプ ファイルは非常に大きなであり、完全なメモリやハンドル テーブルが含まれています。 それ以外の時間が大幅に小さく--のみ 1 つのスレッドに関する情報が含まれて、たとえば、またはのみが、実際にスタックで参照されるモジュールに関する情報が含まれています。

個のミニダンプ ファイルには実際には、「完全」のユーザー モード ダンプより多くの情報が含まれているために、「ミニダンプ」という名前は、誤解を招く。 たとえば、 **.dump/mf**または **.dump/ma**よりも大きいとより完全なファイルが作成されます **.dump/f**します。 このため、 **.dump/m**\[*MiniOptions* \]よりも推奨 **.dump/f**すべてユーザー モード ダンプ ファイルを作成します。

デバッガーでミニダンプ ファイルを作成する場合に含める情報だけを選択できます。 単純な **.dump/m**コマンド ターゲット プロセスのスレッドの情報、およびスタック情報を構成する読み込まれたモジュールに関する基本情報が含まれます。 これは、次のオプションのいずれかを使用して変更できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">.dump オプション</th>
<th align="left">ダンプ ファイルへの影響</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/ma</strong></p></td>
<td align="left"><p>すべての追加のオプションでは、ミニダンプを作成します。 <strong>/Ma</strong>オプションに相当<strong>/mfFhut</strong> --ミニダンプに完全なメモリのデータ、ハンドルのデータ、アンロードされたモジュールは、基本的なメモリについては、およびスレッド時間の情報を追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mf</strong></p></td>
<td align="left"><p>ミニダンプには、完全なメモリのデータを追加します。 ターゲット アプリケーションによって所有されているすべてのアクセス可能なコミットされたページにが含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mF</strong></p></td>
<td align="left"><p>ミニダンプには、すべてのメモリの基本的な情報を追加します。 ミニダンプは、すべての基本的なメモリ情報、有効なメモリについてだけでなく情報を含むストリームに追加します。 これにより、デバッガーは、ミニダンプをデバッグするときに、プロセスの完全な仮想メモリ レイアウトを再構築できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mh</strong></p></td>
<td align="left"><p>ミニダンプにターゲット アプリケーションに関連付けられたハンドルに関するデータを追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mu</strong></p></td>
<td align="left"><p>ミニダンプにアンロードされたモジュールの情報を追加します。 これは、Windows Server 2003 および以降のバージョンの Windows で使用できるのみです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mt</strong></p></td>
<td align="left"><p>ミニダンプには、追加のスレッドの情報を追加します。 これを使用して表示できる、スレッド時間が含まれます<strong><a href="-ttime--display-thread-times-.md" data-raw-source="[.ttime (Display Thread Times)](-ttime--display-thread-times-.md)">.ttime (スレッドの表示時間)</a></strong>ミニダンプをデバッグするときにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mi</strong></p></td>
<td align="left"><p>追加<em>2 次メモリ</em>ミニダンプにします。 セカンダリのメモリはスタックまたはバッキング ストア、およびこのアドレスを囲む小さな領域上のポインターによって参照される任意のメモリです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mp</strong></p></td>
<td align="left"><p>ミニダンプには、プロセスの環境ブロック (PEB) とスレッド環境ブロックの終了のデータを追加します。 これは、アプリケーションのプロセスとスレッドに関する Windows システム情報にアクセスする必要がある場合に役立ちます。 ことができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mw</strong></p></td>
<td align="left"><p>ミニダンプには、すべてのコミットされた読み取り/書き込みプライベート ページを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/md</strong></p></td>
<td align="left"><p>ミニダンプには、実行可能イメージ内のすべての読み取り/書き込みデータ セグメントを追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mc</strong></p></td>
<td align="left"><p>イメージ内のコード セクションを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mr</strong></p></td>
<td align="left"><p>スタック トレースを再作成に適していないスタックとストアのメモリ部分、ミニダンプから削除します。 ローカル変数とその他のデータ型の値がも削除されます。 このオプションは、ミニダンプより小さい (以降、これらのセクションでは単にゼロになります)、メモリが他のアプリケーションのプライバシーを保護する場合に便利です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mR</strong></p></td>
<td align="left"><p>ミニダンプからモジュールの完全なパスを削除します。 モジュールのみ<em>名</em>が含まれます。 これは、ユーザーのディレクトリ構造のプライバシーを保護する場合に便利なオプションです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mk のいずれか"</strong> <em>FileName</em> <strong>"</strong></p></td>
<td align="left"><p>(Windows Vista のみ)ユーザー モードのミニダンプに加えてカーネル モードのミニダンプを作成します。 カーネル モードのミニダンプはユーザー モードのミニダンプに格納されている同じスレッドに限定されます。 <em>ファイル名</em>引用符で囲む必要があります。</p></td>
</tr>
</tbody>
</table>


これらのオプションを組み合わせることができます。 たとえば、次のコマンド **.dump/mfiu**非常に大きなミニダンプ、または、コマンドを作成するために使用できる **.dump/mrR**ユーザーのプライバシーを保持するミニダンプの作成に使用できます。 完全な構文の詳細については、次を参照してください。 [ **.dump (ダンプ ファイルの作成)**](-dump--create-dump-file-.md)します。


## <a name="span-idcreatingspanspan-idcreatingspancreating-a-user-mode-dump-file"></a><span id="creating"></span><span id="CREATING"></span>ユーザー モード ダンプ ファイルを作成します。

ユーザー モード ダンプ ファイルを作成するために使用できるさまざまなツールがいくつかあります。CDB、WinDbg、Windows のエラー報告 (WER)、UserDump、および ADPlus します。

ADPlus をユーザー モード ダンプ ファイルを作成する方法の詳細については、次を参照してください。 [ADPlus](adplus.md)します。

WER を通じてユーザー モード ダンプ ファイルを作成する方法の詳細については、次を参照してください。 [Windows エラー報告](windows-error-reporting.md)します。


## <a name="span-idddkchoosingthebesttooldbgspanspan-idddkchoosingthebesttooldbgspanchoosing-the-best-tool"></a><span id="ddk_choosing_the_best_tool_dbg"></span><span id="DDK_CHOOSING_THE_BEST_TOOL_DBG"></span>最適なツールを選択します。

ユーザー モード ダンプ ファイルを作成できるさまざまなツールがあります。 ほとんどの場合は、ADPlus を使用する最適なツールです。

次の表では、各ツールの機能を示します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">機能</th>
<th align="left"><a href="adplus.md" data-raw-source="[ADPlus](adplus.md)">ADPlus</a></th>
<th align="left"><a href="windows-error-reporting.md" data-raw-source="[Windows Error Reporting](windows-error-reporting.md)">Windows エラー報告</a></th>
<th align="left"><a href="#cdb-windbg" data-raw-source="[CDB and WinDbg](#cdb-windbg)">CDB と WinDbg</a></th>
<th align="left"><a href="#userdump" data-raw-source="[UserDump](#userdump)">UserDump</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ダンプ ファイルを作成して、アプリケーションがクラッシュする (事後分析のデバッグ)</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>はい</p></td>
</tr>
<tr class="even">
<td align="left"><p>アプリケーション「ハング」時にダンプ ファイルを作成する (応答を停止しますが、実際にはクラッシュしていない)</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>はい</p></td>
</tr>
<tr class="odd">
<td align="left"><p>アプリケーションには、例外が発生したときに、ダンプ ファイルを作成します。</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>はい</p></td>
</tr>
<tr class="even">
<td align="left"><p>アプリケーションは正常に実行中に、ダンプ ファイルを作成します。</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>いいえ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>スタートアップ中に失敗したアプリケーションからダンプ ファイルを作成します。</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>はい</p></td>
</tr>
<tr class="even">
<td align="left"><p>既存のダンプ ファイルの圧縮</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 
## <a name="span-idcdb-windbgspanspan-idcdb-windbgspancdb-and-windbg"></a><span id="cdb-windbg"></span><span id="CDB-WINDBG"></span>CDB と WinDbg


CDB と WinDbg できますユーザー モード ダンプ ファイル作成のさまざまな方法で。

### <a name="span-idcreatingadumpfileautomaticallyspanspan-idcreatingadumpfileautomaticallyspancreating-a-dump-file-automatically"></a><span id="creating_a_dump_file_automatically"></span><span id="CREATING_A_DUMP_FILE_AUTOMATICALLY"></span>ダンプ ファイルを自動的に作成します。

アプリケーション エラーが発生する場合は、Windows が事後分析のデバッグ設定に応じて、いくつかの異なる方法で対応できます。 これらの設定は、デバッグ ダンプ ファイルを作成するツールを指示する、ユーザー モードのメモリ ダンプ ファイルが作成されます。 詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。

### <a name="span-idcreatingdumpfileswhiledebuggingspanspan-idcreatingdumpfileswhiledebuggingspancreating-dump-files-while-debugging"></a><span id="creating_dump_files_while_debugging"></span><span id="CREATING_DUMP_FILES_WHILE_DEBUGGING"></span>デバッグ中にダンプ ファイルの作成

CDB または WinDbg ユーザー モード アプリケーションのデバッグは時に、 [ **.dump (ダンプ ファイルの作成)** ](-dump--create-dump-file-.md)ダンプ ファイルを作成するコマンド。

このコマンドは、ターゲット アプリケーションが終了するには発生しません。 適切なコマンドのオプションを選択すると、情報の正確な量を含むミニダンプ ファイルを作成できます。

### <a name="span-idshrinkinganexistingdumpfilespanspan-idshrinkinganexistingdumpfilespanshrinking-an-existing-dump-file"></a><span id="shrinking_an_existing_dump_file"></span><span id="SHRINKING_AN_EXISTING_DUMP_FILE"></span>既存のダンプ ファイルの圧縮

CDB と WinDbg を使用できます*圧縮*ダンプ ファイル。 これを行うには、既存のダンプ ファイルのデバッグを開始しを使用して、 **.dump**小さなサイズのダンプ ファイルを作成するコマンド。


## <a name="span-iduserdumpspanspan-iduserdumpspanuserdump"></a><span id="userdump"></span><span id="USERDUMP"></span>UserDump

UserDump ツール (Userdump.exe) とも呼ばれるユーザー モード プロセスのダンプは、ユーザー モード ダンプ ファイルを作成できます。

UserDump およびそのドキュメントは、OEM サポート ツール パッケージの一部です。

詳細については、これらのツールをダウンロードするを参照してください。 [Userdump.exe ツールを使用して、ダンプ ファイルを作成する方法](https://go.microsoft.com/fwlink/p/?LinkId=241339)し、そのページの指示に従います。 さらに、ときに CDB または WinDbg ユーザー モード アプリケーションのデバッグは、使用することも、 [(ダンプ ファイルの作成) .dump コマンド](-dump--create-dump-file-.md)ダンプ ファイルを作成します。




 





