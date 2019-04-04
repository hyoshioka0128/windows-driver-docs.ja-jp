---
title: Tools.ini を構成します。
description: Tools.ini を構成します。
ms.assetid: 4f0d9f48-99d5-4180-b25d-70fd8de6f20e
keywords:
- tools.ini ファイル
- ntsd.ini ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82c07d43844c941446d93c6646615dc42e84e63d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532289"
---
# <a name="configuring-toolsini"></a>Tools.ini を構成します。


## <span id="ddk_configuring_tools_ini_dbg"></span><span id="DDK_CONFIGURING_TOOLS_INI_DBG"></span>


ファイル tools.ini には、コマンド ライン デバッガーを初期化するために情報が含まれています。 スタートアップ時に、デバッガーは tools.ini ファイル内の適切なセクション ヘッダーを検索し、ヘッダーの下のエントリから初期化情報を抽出します。 各コマンド ライン デバッガーが、独自のセクション ヘッダー - \[CDB\]、 \[NTSD\]、および\[KD\]します。 環境変数の初期化は、tools.ini ファイルを含むディレクトリをポイントする必要があります。

WinDbg は tools.ini ファイルを使用しません。 代わりに、初期化の設定の保存 WinDbg[ワークスペース](using-workspaces.md)します。

Tools.ini エントリは、次の表に表示されます。

キーワードは、値から空白またはコロンで区切る必要があります。 キーワードは区別されません。

**TRUE**または**FALSE** "FALSE"の値は false のみの値。 その他は**TRUE**します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$u0:</strong> <em>値</em>.<strong>ドル u9:</strong> <em>値</em></p></td>
<td align="left"><p>固定名のエイリアスには、値を割り当てます。 数値の値を指定できます<em>n</em>または<em>0xn</em>またはその他の文字列。 参照してください<a href="using-aliases.md" data-raw-source="[Using Aliases](using-aliases.md)">Using エイリアス</a>詳細についてはします。 コマンド ライン コマンドはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>DebugChildren:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 場合<strong>TRUE</strong>CDB は、その可能性がありますを生成するすべての子プロセスと同様に、指定したアプリケーションをデバッグします。 コマンド ライン コマンドは<strong>-o</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DebugOutput:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 場合<strong>TRUE</strong>CDB が出力を送信し、ターミナルからの入力を受け取ります。 場合<strong>FALSE</strong>出力は、ユーザーの画面に移動します。 コマンド ライン オプション<strong>-d</strong>は似ていますが、同一ではないです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IniFile:</strong> <em>ファイル</em></p></td>
<td align="left"><p>か KD、CDB が起動時にコマンドを受け取ることのスクリプト ファイルの名前を指定します。 既定では、現在のディレクトリで ntsd.ini ファイルです。 コマンド ライン コマンドは<strong>cf</strong>します。詳細については、<a href="using-script-files.md" data-raw-source="[Using Script Files](using-script-files.md)">スクリプト ファイルを使用する</a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LazyLoad:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 場合<strong>TRUE</strong>、CDB シンボルの遅延読み込みを実行します。 必要になるまでは、シンボルが読み込まれなかったします。 コマンド ライン コマンドは<strong>-s</strong>します。</p>
<p>詳細、および他の方法でこのオプションを設定では、<a href="deferred-symbol-loading.md" data-raw-source="[Deferred Symbol Loading](deferred-symbol-loading.md)">シンボルの読み込みの遅延</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SetDll:</strong> <em>ファイル名</em></p></td>
<td align="left"><p>拡張 DLL を設定します。 .Dll ファイル名の拡張子を省略する必要があります。 既定では、userexts.dll です。 コマンド ライン コマンドは<strong>-</strong>します。</p>
<p>詳細、およびこの既定の設定の他のメソッドでは、<a href="loading-debugger-extension-dlls.md" data-raw-source="[Loading Debugger Extension DLLs](loading-debugger-extension-dlls.md)">デバッガー拡張 Dll の読み込み</a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>StopFirst:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 場合<strong>true</strong>CDB がイメージの読み込みプロセスの最後に、ブレークポイントで停止します。 コマンド ライン コマンドは<strong>-g</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>StopOnProcessExit:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 場合<strong>TRUE</strong>、プロセス終了の通知を受信したときに CDB が停止します。 コマンド ライン コマンドは<strong>-g</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong>sxd:</strong> <em>event</em>
<strong>sxe:</strong> <em>event</em></td>
<td align="left"><p>応答と、指定した例外またはイベントの処理のステータスは、デバッガーを設定します。</p>
<p>例外とイベントは、次の方法で指定できます。</p>
<p></p>
<strong>*</strong>:既定の例外<em>n</em>:例外<em>n</em> (10 進数) <em>0xn</em>:例外<em>0xn</em> (その他) (16 進)。イベント コード
<p>参照してください<a href="controlling-exceptions-and-events.md" data-raw-source="[Controlling Exceptions and Events](controlling-exceptions-and-events.md)">を制御する例外とイベント</a>このプロセスの詳細と、これらの設定を制御するための他のメソッド。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>VerboseOutput:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 場合<strong>TRUE</strong>、CDB シンボルの処理、イベント通知、およびその他の実行時の出現回数に関する詳細情報が表示されます。 コマンド ライン コマンドは<strong>-v</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>行:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 行のフラグを有効またはソース行情報のサポートを無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srcopt:</strong> <em>options</em></p></td>
<td align="left"><p>ソースのソースの表示とプログラムをステップ実行オプションを制御する行のオプションを設定します。 詳細については、 <strong><a href="l---l---set-source-options-.md" data-raw-source="[l+, l- (Set Source Options)](l---l---set-source-options-.md)">l +、l - (ソース オプションの設定)</a></strong>を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srcpath:</strong> <em>directory</em></p></td>
<td align="left"><p>ソース ファイルの検索パスを設定します。 詳細については、 <strong><a href="-srcpath---lsrcpath--set-source-path-.md" data-raw-source="[.srcpath, .lsrcpath (Set Source Path)](-srcpath---lsrcpath--set-source-path-.md)">.srcpath、.lsrcpath (ソース パスの設定)</a></strong>を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enable_unicode:</strong> <em>flag</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 Enable_unicode フラグは、デバッガーが Unicode 文字列として、USHORT ポインターと配列を表示するかどうかを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>force_radix_output:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 Force_radix_output フラグは、10 進形式または既定の基数で整数を表示するかどうかを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>col_mode:</strong> <em>フラグ</em></p></td>
<td align="left"><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 Col_mode フラグは、[カラー] モード設定を制御します。 色のモードが有効にすると、デバッガーは、色付きの出力を生成できます。 既定では、大部分の色が設定されていないと、現在のコンソールの色を既定の代わりにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>col:</strong> <em>name</em> <em>colspec</em></p></td>
<td align="left"><p><em>名前</em>色分けは要素を示します。 <em>Colspec</em>フォーム [rR-] [gG-] [bB-] の 3 文字の RGB インジケーターです。 小文字の文字が濃くなるほどを示します、大文字 brighter 示しダッシュにないコンポーネントの色の効果ことを示します。 コンソールの色が原因は、制限事項、明るいは実際には、コンポーネントごとではありませんが、明るいいずれかを要求した場合、すべてのコンポーネントに適用されます。 つまり、rgB は RGB の場合と同じです。 このため、任意の大文字が使用する場合に、すべて大文字を使用することをお勧めします。</p>
<p>使用例:</p>
<p>col: emphfg R--</p></td>
</tr>
</tbody>
</table>

 

サンプル\[NTSD\] tools.ini ファイルのセクションに従います。

```inf
[NTSD]
sxe: 3c
sxe: cc
$u0: VeryLongName
VerboseOutput:true
```

 

 





