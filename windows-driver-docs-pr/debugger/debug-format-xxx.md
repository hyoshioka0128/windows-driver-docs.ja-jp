---
title: デバッグ\_形式\_XXX
description: DEBUG_FORMAT_XXX ビットフラグは、WriteDumpFile2 および WriteDumpFileWide がクラッシュダンプファイルの形式を決定するために使用されます。また、ユーザーモードミニダンプの場合は、ファイルに含める情報を指定します。
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
ms.openlocfilehash: 60aa527199b5fe2b395200fdf2dd8b059e7794e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837794"
---
# <a name="debug_format_xxx"></a>デバッグ\_形式\_XXX

DEBUG_FORMAT_XXX ビットフラグは、WriteDumpFile2 および WriteDumpFileWide がクラッシュダンプファイルの形式を決定するために使用されます。また、ユーザーモードミニダンプの場合は、ファイルに含める情報を指定します。

次のビットフラグは、すべてのクラッシュダンプファイルに適用されます。

<table>
<tr>
<th>Value</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_WRITE_CAB</p>
</td>
<td>
<p>クラッシュダンプファイルを CAB ファイルにパッケージ化します。  指定されたファイル名またはファイルハンドルは、CAB ファイルに使用されます。クラッシュダンプは、CAB ファイルに移動される前に、一時ファイルに最初に作成されます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_CAB_SECONDARY_FILES</p>
</td>
<td>
<p>
<dl>
<dt>現在のシンボルとマップされたイメージを CAB ファイルに含めます。</dt>
<dt>DEBUG_FORMAT_WRITE_CAB が設定されていない場合、このフラグは無視されます。</dt>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_NO_OVERWRITE</p>
</td>
<td>
<p>既存のファイルは上書きしないでください。</p>
</td>
</tr>
</table>
<p> </p>
<p>ユーザーモードミニダンプには、次のビットフラグを含めることもできます。</p>
<table>
<tr>
<th>Value</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY</p>
</td>
<td>
<p>メモリの完全なデータを追加します。  ターゲットアプリケーションが所有している、アクセス可能なすべてのコミット済みページが含まれます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_HANDLE_DATA</p>
</td>
<td>
<p>ターゲットアプリケーションに関連付けられているハンドルに関するデータを追加します。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_UNLOADED_MODULES</p>
</td>
<td>
<p>アンロードされたモジュール情報を追加します。  この情報は、Windows Server 2003 以降のバージョンの Windows でのみ使用できます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_INDIRECT_MEMORY</p>
</td>
<td>
<p>間接メモリを追加します。  スタックまたはバッキングストアのポインターによって参照される任意のアドレスを囲むメモリの小さな領域が含まれます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_DATA_SEGMENTS</p>
</td>
<td>
<p>実行可能イメージ内のすべてのデータセグメントを追加します。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_MEMORY</p>
</td>
<td>
<p>スタックトレースの再作成には役立たないスタックおよびバッキングストアのすべてのメモリをゼロに設定します。  これにより、ミニダンプをより効率的に圧縮し、不要な情報を削除することでプライバシーを向上させることができます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_PATHS</p>
</td>
<td>
<p>モジュール名だけを残してモジュールパスを削除します。  これは、ディレクトリ構造 (ユーザーの名前が含まれている場合もあります) を非表示にすることによって、プライバシーを保護するために役立ちます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_TRIAGE</p>
</td>
<td>
<p>この形式は、ダンプでキャプチャされた他のデータへのポインターではないデータを除外するために使用されます。 フラグを使用して、ダンプに存在するプライベートデータの量を減らしながら、クラッシュを診断できるようにすることができます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_PROCESS_THREAD_DATA</p>
</td>
<td>
<p>プロセス環境ブロック (PEB) とスレッド環境ブロック (TEB) を追加します。  このフラグは、スレッドとプロセスの Windows システム情報を提供するために使用できます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_PRIVATE_READ_WRITE_MEMORY</p>
</td>
<td>
<p>コミットされたすべてのプライベート読み取り/書き込みメモリページを追加します。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_NO_OPTIONAL_DATA</p>
</td>
<td>
<p>
<dl>
<dt>プライバシーを重視したデータがミニダンプに含まれないようにします。 現在、このフラグは、次のフラグが設定されているために追加されたミニダンプデータから除外されます:</dt>
<dt>DEBUG_FORMAT_USER_SMALL_PROCESS_THREAD_DATA、</dt>
<dt>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY、</dt>
<dt>DEBUG_FORMAT_USER_SMALL_INDIRECT_MEMORY、</dt>

<dt>DEBUG_FORMAT_USER_SMALL_PRIVATE_READ_WRITE_MEMORY</dt></dl>
</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY_INFO</p>
</td>
<td>
<p>すべての基本的なメモリ情報を追加します。  これは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces2-queryvirtual" data-raw-source="[IDebugDataSpaces2::QueryVirtual method](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces2-queryvirtual)">IDebugDataSpaces2:: QueryVirtual メソッド</a>によって返される情報です。  有効なメモリだけでなく、すべてのメモリの情報が含まれています。これにより、デバッガーはミニダンプから完全な仮想メモリレイアウトを再構築できます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_THREAD_INFO</p>
</td>
<td>
<p>スレッド情報を追加します。これには、実行時間、開始時刻、終了時刻、開始アドレス、終了状態が含まれます。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_CODE_SEGMENTS</p>
</td>
<td>
<p>実行可能イメージを含むすべてのコードセグメントを追加します。</p>
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
<td align="left">DbgEng .h (DbgEng .h を含む)</td>
</tr>
</tbody>
</table>
 





