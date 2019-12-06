---
title: ユーザーモード ダンプ ファイル
description: ユーザーモード ダンプ ファイル
ms.assetid: bef29d75-6620-4219-b402-36fbddc4fe1f
keywords:
- ダンプファイル、ユーザーモード
ms.date: 12/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: a0d2f9e217d5d33331924d6f6619335eed8a0371
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74861927"
---
# <a name="user-mode-dump-files"></a>ユーザーモード ダンプ ファイル

このセクションの内容:

- [ユーザーモードのダンプファイルの種類](#varieties)

- [ユーザーモードのダンプファイルを作成する](#creating)

ダンプファイルの分析の詳細については、「[ユーザーモードのダンプファイルの分析](analyzing-a-user-mode-dump-file.md)」を参照してください。

## <a name="span-idvarietiesspanspan-idvarietiesspan-varieties-of-user-mode-dump-files"></a><span id="varieties"></span><span id="VARIETIES"></span>ユーザーモードのダンプファイルの種類

ユーザーモードのクラッシュダンプファイルにはいくつかの種類がありますが、次の2つのカテゴリに分けられています。

[完全なユーザーモードダンプ](#full)

[ミニダンプ](#minidumps)

これらのダンプファイルの違いは、サイズの1つです。 ミニダンプは通常、よりコンパクトで、アナリストに簡単に送信できます。

**注**   ダンプファイルを分析することで、多くの情報を取得できます。 ただし、デバッガーを使用して直接クラッシュをデバッグするのと同じほど多くの情報をダンプファイルに提供できません。

## <a name="span-idfullspanspan-idfullspanfull-user-mode-dumps"></a><span id="full"></span><span id="FULL"></span>完全なユーザーモードダンプ

*完全なユーザーモードダンプ*は、ユーザーモードの基本ダンプファイルです。

このダンプファイルには、プロセスのメモリ領域全体、プログラムの実行可能イメージ自体、ハンドルテーブル、およびダンプの発生時に使用されていたメモリを再構築する際にデバッガーに役立つその他の情報が含まれています。

完全なユーザーモードのダンプファイルをミニダンプに "圧縮" できます。 単純にダンプファイルをデバッガーに読み込んでから、.dump [ **(ダンプファイルの作成)** ](-dump--create-dump-file-.md)コマンドを使用して、新しいダンプファイルをミニダンプ形式で保存します。

**メモ**   名前にかかわらず、最大の "ミニダンプ" ファイルには、完全なユーザーモードダンプよりも多くの情報が含まれています。 たとえば、 **. dump/mf**または **. dump/ma**では、 **. dump/f**よりも大規模で完全なファイルが作成されます。

ユーザーモードでは、 **. dump/m\[** <em>minioptions</em> **\]** が最適な選択肢です。 このスイッチを使用して作成されたダンプファイルのサイズは、非常に小さいものから大きくなる場合があります。 適切な*Minioptions*を指定することによって、含まれる情報を正確に制御できます。

## <a name="span-idminidumpsspanspan-idminidumpsspanminidumps"></a><span id="minidumps"></span><span id="MINIDUMPS"></span>ミニダンプ

プロセスに関連付けられているメモリの選択した部分のみを含むユーザーモードのダンプファイルは、*ミニダンプ*と呼ばれます。

ミニダンプファイルのサイズと内容は、ダンプするプログラムとダンプを実行するアプリケーションによって異なります。 ミニダンプファイルのサイズが非常に大きく、完全なメモリとハンドルのテーブルが含まれていることがあります。 それ以外の場合は、非常に小さくなります。たとえば、1つのスレッドに関する情報のみが含まれている場合や、実際にスタック内で参照されているモジュールに関する情報のみが含まれている場合などです。

最大のミニダンプファイルには、"完全な" ユーザーモードダンプよりも多くの情報が含まれているため、"ミニダンプ" という名前は誤解を招くことがあります。 たとえば、 **. dump/mf**または **. dump/ma**では、 **. dump/f**よりも大規模で完全なファイルが作成されます。 このため、 **. dump/m**\[*minioptions*\] 推奨さ**れています。** すべてのユーザーモードダンプファイルを作成するにはダンプ/f を使用してください。

デバッガーでミニダンプファイルを作成する場合は、どのような情報を含めるかを正確に選択できます。 単純な **.dump/m**コマンドには、対象プロセス、スレッド情報、およびスタック情報を構成する、読み込まれたモジュールに関する基本情報が含まれます。 これは、次のいずれかのオプションを使用して変更できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">. dump オプション</th>
<th align="left">ダンプファイルへの影響</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/ma</strong></p></td>
<td align="left"><p>すべてのオプションの追加を使用してミニダンプを作成します。 <strong>/Ma</strong>オプションは、 <strong>/mfFhut</strong>に相当します。これは、完全なメモリデータの追加、データの処理、モジュール情報のアンロード、基本的なメモリ情報、およびスレッド時間情報をミニダンプに追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mf</strong></p></td>
<td align="left"><p>ミニダンプにメモリデータ全体を追加します。 ターゲットアプリケーションが所有している、アクセス可能なすべてのコミット済みページが含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mF</strong></p></td>
<td align="left"><p>すべての基本メモリ情報をミニダンプに追加します。 これにより、有効なメモリに関する情報だけでなく、すべての基本的なメモリ情報を含むミニダンプにストリームが追加されます。 これにより、ミニダンプのデバッグ中に、デバッガーがプロセスの完全な仮想メモリレイアウトを再構築できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mh</strong></p></td>
<td align="left"><p>ターゲットアプリケーションに関連付けられているハンドルに関するデータをミニダンプに追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mu</strong></p></td>
<td align="left"><p>アンロードされたモジュール情報をミニダンプに追加します。 これは、Windows Server 2003 以降のバージョンの Windows でのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mt</strong></p></td>
<td align="left"><p>ミニダンプにスレッド情報を追加します。 これには、ミニダンプのデバッグ時に<strong><a href="-ttime--display-thread-times-.md" data-raw-source="[.ttime (Display Thread Times)](-ttime--display-thread-times-.md)">. ttime (スレッド時間を表示)</a></strong>を使用して表示できるスレッド時刻が含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mi</strong></p></td>
<td align="left"><p>ミニダンプに<em>セカンダリメモリ</em>を追加します。 セカンダリメモリは、スタックまたはバッキングストアのポインターによって参照される任意のメモリと、このアドレスを囲む小さい領域で参照されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mp</strong></p></td>
<td align="left"><p>プロセス環境ブロック (PEB) とスレッド環境ブロック (TEB) のデータをミニダンプに追加します。 これは、アプリケーションのプロセスとスレッドに関する Windows システム情報にアクセスする必要がある場合に便利です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mw</strong></p></td>
<td align="left"><p>コミットされたすべての読み取り/書き込みプライベートページをミニダンプに追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/md</strong></p></td>
<td align="left"><p>実行可能イメージ内のすべての読み取り/書き込みデータセグメントをミニダンプに追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mc corelibc.lib で</strong></p></td>
<td align="left"><p>イメージ内にコードセクションを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mr</strong></p></td>
<td align="left"><p>スタックの各部分をミニダンプから削除し、スタックトレースの再作成には役立たないメモリを格納します。 ローカル変数とその他のデータ型の値も削除されます。 このオプションではミニダンプは小さくなりません (これらのメモリセクションは単にゼロになっているため)。ただし、他のアプリケーションのプライバシーを保護する場合に便利です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mR</strong></p></td>
<td align="left"><p>ミニダンプから完全なモジュールパスを削除します。 モジュール<em>名</em>だけが含まれます。 これは、ユーザーのディレクトリ構造のプライバシーを保護する場合に便利なオプションです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mk "</strong> <em>FileName</em> <strong>"</strong></p></td>
<td align="left"><p>(Windows Vista のみ)ユーザーモードミニダンプに加えて、カーネルモードミニダンプを作成します。 カーネルモードミニダンプは、ユーザーモードミニダンプに格納されているのと同じスレッドに制限されます。 <em>ファイル名</em>は引用符で囲む必要があります。</p></td>
</tr>
</tbody>
</table>

これらのオプションは組み合わせて使用できます。 たとえば、 **/mfiu**を使用すると、非常に大きなミニダンプやコマンドを作成でき**ます。 dump/mrR**を使用すると、ユーザーのプライバシーを維持するミニダンプを作成できます。 完全な構文の詳細については、「[**ダンプ (ダンプファイルの作成)** ](-dump--create-dump-file-.md)」を参照してください。

## <a name="span-idcreatingspanspan-idcreatingspancreating-a-user-mode-dump-file"></a><span id="creating"></span><span id="CREATING"></span>ユーザーモードのダンプファイルを作成する

ユーザーモードのダンプファイルの作成に使用できるツールには、CDB、WinDbg、Procdump のいくつかがあります。

## <a name="span-idprocdumpspanspan-idprocdumpspanprocdump"></a><span id="procdump"></span><span id="Procdump"></span>ProcDump

ProcDump は、CPU スパイクのためにアプリケーションを監視し、管理者または開発者がスパイクの原因を特定するために使用できるスパイク中にクラッシュダンプを生成することを主な目的としているコマンドラインユーティリティです。 また、ProcDump には、ハングしたウィンドウの監視 (Windows およびタスクマネージャーが使用するウィンドウのハングと同じ定義を使用)、未処理の例外監視、システムパフォーマンスカウンターの値に基づいたダンプの生成が含まれます。 また、他のスクリプトに埋め込むことができる一般的なプロセスダンプユーティリティとしても使用できます。

Sysinternals ProcDump ユーティリティを使用してユーザーモードのダンプファイルを作成する方法の詳細については、「 [ProcDump](https://docs.microsoft.com/sysinternals/downloads/procdump)」を参照してください。

## <a name="span-idcdb-windbgspanspan-idcdb-windbgspancdb-and-windbg"></a><span id="cdb-windbg"></span><span id="CDB-WINDBG"></span>CDB と WinDbg

CDB と WinDbg では、さまざまな方法でユーザーモードのダンプファイルを作成できます。

### <a name="span-idcreating_a_dump_file_automaticallyspanspan-idcreating_a_dump_file_automaticallyspancreating-a-dump-file-automatically"></a><span id="creating_a_dump_file_automatically"></span><span id="CREATING_A_DUMP_FILE_AUTOMATICALLY"></span>ダンプファイルを自動的に作成する

アプリケーションエラーが発生すると、Windows は、事後分析のデバッグ設定に応じて、いくつかの異なる方法で応答できます。 これらの設定によって、ダンプファイルを作成するようにデバッグツールに指示された場合は、ユーザーモードのメモリダンプファイルが作成されます。 詳細については、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。

### <a name="span-idcreating_dump_files_while_debuggingspanspan-idcreating_dump_files_while_debuggingspancreating-dump-files-while-debugging"></a><span id="creating_dump_files_while_debugging"></span><span id="CREATING_DUMP_FILES_WHILE_DEBUGGING"></span>デバッグ中のダンプファイルの作成

CDB または WinDbg がユーザーモードアプリケーションをデバッグしている場合は、.dump [ **(ダンプファイルの作成)** ](-dump--create-dump-file-.md)コマンドを使用してダンプファイルを作成することもできます。

このコマンドを実行しても、ターゲットアプリケーションは終了しません。 適切なコマンドオプションを選択することで、必要な量の情報を正確に含むミニダンプファイルを作成できます。

### <a name="span-idshrinking_an_existing_dump_filespanspan-idshrinking_an_existing_dump_filespanshrinking-an-existing-dump-file"></a><span id="shrinking_an_existing_dump_file"></span><span id="SHRINKING_AN_EXISTING_DUMP_FILE"></span>既存のダンプファイルを圧縮する

CDB と WinDbg を使用してダンプファイルを*圧縮*することもできます。 これを行うには、既存のダンプファイルのデバッグを開始してから、.dump コマンドを使用してサイズの小さいダンプファイルを作成し**ます**。

## <a name="span-idcdb-windbgspanspan-idcdb-windbgspan-time-travel-debugging-ttd"></a><span id="cdb-windbg"></span><span id="CDB-WINDBG"></span>タイムトラベルデバッグ (TTD)

CDB、WinDbg、Procdump に加えて、ユーザーモードアプリケーションをデバッグするためのもう1つのオプションは、タイムトラベルデバッグ (TTD) です。 タイムトラベルデバッグは、実行中のプロセスの実行を記録し、後で前後に再生できるツールです。 タイムトラベルデバッグ (TTD) を使用すると、バグが見つかるまで問題を再現するのではなく、デバッガーセッションを "巻き戻し" することで、問題を簡単にデバッグできます。

TTD を使用すると、バグにつながる条件をより深く理解し、それを複数回再生して問題の解決に最適な方法を知ることができます。

TTD には、クラッシュダンプファイルよりも利点があります。多くの場合、最終的な障害につながるコード実行が欠落しています。

タイムトラベルデバッグ (TTD) の詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。
