---
title: カーネルモードの環境変数
description: カーネルモードの環境変数
ms.assetid: 619ebe55-1b57-4182-ada9-0c99c78056b3
keywords:
- environment variables, kernel-mode
- _NT_DEBUG_PORT 環境変数
- _NT_DEBUG_BAUD_RATE 環境変数
- KDQUIET 環境変数
- _NT_DEBUG_CACHE_SIZE 環境変数
- _NT_DEBUG_BUS 環境変数
- _NT_DEBUG_1394_CHANNEL 環境変数
- _NT_DEBUG_1394_SYMLINK environment variable
- _NT_DEBUG_OPTIONS 環境変数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e16627de75b81be5d8429ff9f1150df4be288670
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581989"
---
# <a name="kernel-mode-environment-variables"></a>カーネルモードの環境変数


## <span id="ddk_kernel_mode_environment_variables_dbg"></span><span id="DDK_KERNEL_MODE_ENVIRONMENT_VARIABLES_DBG"></span>


次の表は、カーネル モードのデバッグでのみ使用されている環境変数を一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">変数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_PORT = <em>comPort</em></p></td>
<td align="left"><p>カーネルの接続で使用する COM ポートを指定します。 詳細については、次を参照してください。<a href="getting-set-up-for-debugging.md" data-raw-source="[Getting Set Up for Debugging](getting-set-up-for-debugging.md)">を取得する設定をデバッグ用</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_BAUD_RATE = <em>BaudRate</em></p></td>
<td align="left"><p>COM ポートの接続経由で使用するボー レートを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_BUS 1394 を =</p></td>
<td align="left"><p>1394 ケーブルの接続経由でカーネル デバッグを行う、ことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_1394_CHANNEL = <em>1394Channel</em></p></td>
<td align="left"><p>1394 カーネルの接続に使用するチャネルを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_1394_SYMLINK = <em>Protocol</em></p></td>
<td align="left"><p>1394 カーネルの接続に使用する接続プロトコルを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KDQUIET =<em>何か</em></p></td>
<td align="left"><p>KDQUIET が定義されている場合、デバッガーで実行されます<em>quiet モード</em>します。 Quiet モードには、次の 3 つの個別の効果が含まれます。</p>
<p>1. デバッガーでは、拡張 DLL がロードまたはアンロードされるたびにメッセージを表示しません。</p>
<p>2. <strong><a href="r--registers-.md" data-raw-source="[r (Registers)](r--registers-.md)">R (レジスタ)</a></strong>コマンドには、不要になったその構文内で等号 (=) が必要です。</p>
<p>3. デバッガーでは、ターゲット コンピューターに中断するときに警告メッセージは表示されません。</p>
<p>使用して非表示モードを制御することも、 <strong><a href="sq--set-quiet-mode-.md" data-raw-source="[sq (Set Quiet Mode)](sq--set-quiet-mode-.md)">sq (非表示モードの設定)</a></strong>コマンド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
_NT_DEBUG_CACHE_SIZE= <em>サイズ</em></td>
<td align="left"><p>最大カーネル キャッシュ サイズ (バイト) を指定します。 このキャッシュは、シリアル接続から、ホスト コンピューターで受信したデータを保持します。 既定では 1,024,000 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_OPTIONS =<em>オプション</em></p></td>
<td align="left"><p>次の 2 つの値のいずれかを指定します。</p>
<p>NOEXTWARNING は、拡張機能コマンドが見つからない場合に警告を出力しないようデバッガーに指示します。</p>
<p>NOVERSIONCHECK は、デバッガーの拡張機能のバージョンを確認しないようにデバッガーに指示します。</p>
<p></p>
<p>これらのオプションを変更またはを使用して表示できます、 <strong><a href="so--set-kernel-debugging-options-.md" data-raw-source="[so (Set Kernel Options)](so--set-kernel-debugging-options-.md)">ため (カーネル オプションの設定)</a></strong> コマンド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_KD_FILES = <em>MapFile</em></p></td>
<td align="left"><p>ドライバーの置換のマップ ファイルを指定します。 詳細については、および他のドライバーの置換を制御する方法については、「<a href="mapping-driver-files.md" data-raw-source="[Mapping Driver Files](mapping-driver-files.md)">ドライバー ファイルのマッピング</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





