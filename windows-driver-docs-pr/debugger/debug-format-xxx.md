---
title: デバッグ\_形式\_XXX
description: DEBUG_FORMAT_XXX のビット フラグは、クラッシュ ダンプ ファイルとユーザー モードのミニダンプをファイルに含めるには、どのような情報の形式を特定 WriteDumpFile2 と WriteDumpFileWide によって使用されます。
ms.date: 08/20/2018
topic_type:
- apiref
api_name:
- DEBUG_FORMAT_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 429a2f8164504b133bb7e02beb60fff5ff012413
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371712"
---
# <a name="debugformatxxx"></a>デバッグ\_形式\_XXX

DEBUG_FORMAT_XXX のビット フラグは、クラッシュ ダンプ ファイルとユーザー モードのミニダンプをファイルに含めるには、どのような情報の形式を特定 WriteDumpFile2 と WriteDumpFileWide によって使用されます。

次のビット フラグは、すべてのクラッシュ ダンプ ファイルに適用されます。

<table>
<tr>
<th>値</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_WRITE_CAB</p>
</td>
<td>
<p>CAB ファイルにクラッシュ ダンプ ファイルをパッケージ化します。  指定されたファイル名またはファイル ハンドルが CAB ファイルの使用します。クラッシュ ダンプは、CAB ファイルに移動される前に一時ファイルに最初に作成されます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_CAB_SECONDARY_FILES</p>
</td>
<td>
<p>
<dl>
<dt>CAB ファイルには、現在のシンボルとマップされたイメージが含まれます。</dt>
<dt>場合 DEBUG_FORMAT_WRITE_CAB が設定されていない、このフラグは無視されます。</dt>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_NO_OVERWRITE</p>
</td>
<td>
<p>既存のファイルを上書きしません。</p>
</td>
</tr>
</table>
<p> </p>
<p>次のビット フラグは、ユーザー モードのミニダンプを含めることもできます。</p>
<table>
<tr>
<th>値</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY</p>
</td>
<td>
<p>完全なメモリのデータを追加します。  ターゲット アプリケーションによって所有されているすべてのアクセス可能なコミットされたページにが含まれます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_HANDLE_DATA</p>
</td>
<td>
<p>ターゲット アプリケーションに関連付けられているハンドルに関するデータを追加します。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_UNLOADED_MODULES</p>
</td>
<td>
<p>アンロードされたモジュールの情報を追加します。  この情報は、Windows Server 2003 および Windows の以降のバージョンでのみ使用できます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_INDIRECT_MEMORY</p>
</td>
<td>
<p>間接メモリを追加します。  任意の stack またはバッキング ストアのポインターによって参照されるアドレスで囲まれているメモリの小さな領域が含まれます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_DATA_SEGMENTS</p>
</td>
<td>
<p>実行可能イメージ内のすべてのデータ セグメントを追加します。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_MEMORY</p>
</td>
<td>
<p>すべてのスタック トレースを再作成するために便利ですが、バッキング ストアとスタックにメモリを 0 に設定します。  これは、ミニダンプの圧縮の効率、不要な情報を削除してプライバシーを増やします。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_PATHS</p>
</td>
<td>
<p>モジュール名のみを残して、モジュールのパスを削除します。  これは (これは、ユーザーの名前を含めることができます)、ディレクトリ構造を非表示にしてプライバシーを保護するために役立ちます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_TRIAGE</p>
</td>
<td>
<p>この形式は、ダンプにキャプチャされたその他のデータへのポインターでないデータをフィルター処理に使用されます。 一方、クラッシュを診断するダンプに存在する個人データの量を削減するフラグを使用できます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_PROCESS_THREAD_DATA</p>
</td>
<td>
<p>プロセスの環境ブロック (PEB) とスレッド環境ブロックの終了を追加します。  スレッドとプロセスの Windows システム情報を提供する、このフラグを使用できます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_PRIVATE_READ_WRITE_MEMORY</p>
</td>
<td>
<p>コミットされたすべての読み取り/書き込みのプライベート メモリのページを追加します。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_NO_OPTIONAL_DATA</p>
</td>
<td>
<p>
<dl>
<dt>プライバシーに機微なデータが、ミニダンプに含まれないようにします。現時点では、このフラグは、次のフラグが設定されているため追加されたミニダンプ データからは含まれません:</dt>
<dt>DEBUG_FORMAT_USER_SMALL_PROCESS_THREAD_DATA、</dt>
<dt>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY、</dt>
<dt>DEBUG_FORMAT_USER_SMALL_INDIRECT_MEMORY、</dt>
<dt>DEBUG_FORMAT_USER_SMALL_PRIVATE_READ_WRITE_MEMORY します。</dt>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY_INFO</p>
</td>
<td>
<p>すべてのメモリの基本的な情報を追加します。  これは、によって返される情報、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces2-queryvirtual" data-raw-source="[IDebugDataSpaces2::QueryVirtual method](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces2-queryvirtual)">IDebugDataSpaces2::QueryVirtual メソッド</a>します。  すべてのメモリの情報は、使用すると、ミニダンプから完全な仮想メモリ レイアウトを再構築デバッガー包含している有効なメモリです。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_THREAD_INFO</p>
</td>
<td>
<p>実行時間を含む追加のスレッドの情報を追加、開始時刻、終了時間、開始アドレス、および状態を終了します。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_CODE_SEGMENTS</p>
</td>
<td>
<p>実行可能イメージを持つすべてのコード セグメントを追加します。</p>
</td>
</tr>
</table>



<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h (DbgEng.h を含む)</td>
</tr>
</tbody>
</table>
 





