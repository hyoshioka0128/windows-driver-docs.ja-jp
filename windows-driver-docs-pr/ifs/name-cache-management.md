---
title: 名前のキャッシュ管理
description: 名前のキャッシュ管理
ms.assetid: 3e1b1419-320e-44e0-a6c2-823517cf07c7
keywords:
- RDBSS WDK ファイル システム、名のキャッシュ
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、名のキャッシュ
- NAME_CACHE 構造体
- WDK RDBSS 名
- キャッシュ WDK RDBSS
- ファイルが見つかりませんメッセージ WDK RDBSS
- WDK RDBSS 名のキャッシュ
- NAME_CACHE_CONTROL 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1378c193d689f211b95aeaea7cf3e12575e9056
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553671"
---
# <a name="name-cache-management"></a>名前のキャッシュ管理


## <span id="ddk_name_cache_management_if"></span><span id="DDK_NAME_CACHE_MANAGEMENT_IF"></span>


名前\_キャッシュ構造キャッシュ名の文字列の最近の操作がサーバーで実行されるため、クライアントは、冗長な要求を抑制できます。 たとえば、最近「ファイルが見つかりません」メッセージで失敗しました、オープンの要求とクライアント アプリケーションは、大文字の文字列でもう一度要求をオープンを試行してネットワークのミニ リダイレクターは大文字と小文字をサポートしていません、RDBSS が失敗要求直後になしで、サーバーをヒットします。

名前に時間のウィンドウと操作数の上限を配置する、アルゴリズムは、一般に、\_キャッシュ エントリ。 時間枠は、通常は 2 秒です。 その場合、名前\_キャッシュ エントリが 2 秒より大きい、一致は失敗し、要求は、サーバーに移動します。 要求は、サーバーの名前でもう一度失敗\_キャッシュ エントリが別の 2 秒間ウィンドウで更新されます。 要求操作の数が一致しないかどうかは、この名前になることがサーバーに送信された 1 つまたは複数の要求\_キャッシュ エントリが無効です。 繰り返しますが、この操作は、サーバーに送信されます。

名前\_キャッシュ構造がネットワーク ミニ-リダイレクター、MRX に公開されるパブリック部分\_名前\_キャッシュ、および RDBSS でのみ使用するためのプライベート セクション。 ミニ リダイレクター部分がコンテキスト フィールド NTSTATUS、いくつか追加ミニリダイレクター特定ストレージの名前の割り当てを併置できますこの名前エントリおよびコンテキスト拡張機能へのポインターに以前のサーバー操作の結果の\_キャッシュの構造体。 詳細については、次を参照してください。 [ **RxNameCacheInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff554586)します。

SMB 操作の数は MRX のコンテキストのフィールドに保存できませんでした、ミニ固有リダイレクターの状態の例を Windows ネットワークの\_名前\_キャッシュします。 ときに[ **RxNameCacheCheckEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554558)が呼び出されると、コンテキスト フィールドと名前キャッシュ内の一致の検索の一部として指定されたパラメーターの間の等価性チェックが実行されます。 名前と\_ネットワーク ミニリダイレクターのジョブ (秒) の名前でこのフィールドを有効期間の適切な値を指定すると、キャッシュ エントリが作成または更新\_キャッシュ エントリ。

名前のプライベート RDBSS 部分\_キャッシュ構造に含まれる、名前、速度の参照名のハッシュ値を Unicode 文字列として、エントリと、サーバーが大文字と小文字をサポートしているかどうかを示すフラグの有効期限。

名前\_キャッシュ\_制御構造は、指定した名前キャッシュを管理します。 フリー リスト、アクティブな一覧をおよび更新を同期するロックがあります。 名前\_キャッシュ\_制御構造も名前の現在の数を格納するフィールドを持つ\_キャッシュ エントリを割り当て、割り当てられる、サイズ、追加のエントリの最大数の値それぞれの名前に使用されるネットワーク-ミニリダイレクター ストレージ\_キャッシュ エントリ、および統計情報 (キャッシュが更新された回数の合計チェック、有効な一致が返され、およびネットワーク ミニ リダイレクターがネットワーク操作を保存する場合) の値。 **MaximumEntries**フィールド名の数の制限\_プログラムを適切に動作しない場合に作成されたキャッシュ エントリが大量のメモリを消費する悪意のあるファイル名を持つオープン要求の数が多いを生成します。

現在はオブジェクトの RDBSS によって管理される名前キャッシュ\_名前\_いない\_が見つかりました。 この名前キャッシュ 2 秒間ウィンドウが保持され、いずれかの操作がサーバーに送信される場合は無効にします。 これでした発生 (サンプル 1) ファイルをクライアント アプリケーションがある、サーバー上のアプリケーションが別のファイル (sample2) の作成に使用できるサーバーでを開きます。 クライアントは、(サンプル 1) 最初のファイルを読み取るし、(サンプル 2) の 2 番目のファイルがサーバーで作成されたことを学習、2 番目のファイル (sample2) に一致する名前のキャッシュのヒット エラーを返すことはできません。 この最適化は、連続するファイルを開く操作がまだ存在しないを同じファイルでの大文字と小文字のみを処理します。 このシナリオでは、Microsoft Word を使用して行われます。

RDBSS 名のキャッシュ管理ルーチンを以下に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554552" data-raw-source="[&lt;strong&gt;RxNameCacheActivateEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554552)"><strong>RxNameCacheActivateEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、名のキャッシュ エントリを取得し、有効期限の時間とネットワーク ミニリダイレクター コンテキストを更新します。 アクティブ リストのエントリが置かれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554558" data-raw-source="[&lt;strong&gt;RxNameCacheCheckEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554558)"><strong>RxNameCacheCheckEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、有効性を NAME_CACHE エントリを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554565" data-raw-source="[&lt;strong&gt;RxNameCacheCreateEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554565)"><strong>RxNameCacheCreateEntry</strong></a></p></td>
<td align="left"><p>このルーチンでは、割り当て、指定した名前の文字列を含む NAME_CACHE 構造体を初期化します。 呼び出し元が名前のキャッシュ コンテキストの追加のネットワーク ミニリダイレクター要素を初期化し、名前キャッシュ アクティブ リストにエントリを配置が必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554569" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554569)"><strong>RxNameCacheExpireEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、フリー リストに NAME_CACHE エントリを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554570" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntryWithShortName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554570)"><strong>RxNameCacheExpireEntryWithShortName</strong></a></p></td>
<td align="left"><p>このルーチンでは、すべて名前プレフィックスには、指定した短いファイル名が一致する NAME_CACHE エントリの有効期限です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554573" data-raw-source="[&lt;strong&gt;RxNameCacheFetchEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554573)"><strong>RxNameCacheFetchEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリの指定した名前の文字列での一致を検索します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554575" data-raw-source="[&lt;strong&gt;RxNameCacheFinalize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554575)"><strong>RxNameCacheFinalize</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE_CONTROL 構造に関連付けられた NAME_CACHE エントリのすべての記憶域を解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554579" data-raw-source="[&lt;strong&gt;RxNameCacheFreeEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554579)"><strong>RxNameCacheFreeEntry</strong></a></p></td>
<td align="left"><p>このルーチンは NAME_CACHE エントリの記憶域を解放し、デクリメント NAME_CACHE_CONTROL 構造に関連付けられているエントリをキャッシュする NAME_CACHE の数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554586" data-raw-source="[&lt;strong&gt;RxNameCacheInitialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554586)"><strong>RxNameCacheInitialize</strong></a></p></td>
<td align="left"><p>このルーチンでは、名前のキャッシュ (NAME_CACHE_CONTROL 構造) を初期化します。</p></td>
</tr>
</tbody>
</table>

 

 

 




