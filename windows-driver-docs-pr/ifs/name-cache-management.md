---
title: 名前キャッシュ管理
description: 名前キャッシュ管理
ms.assetid: 3e1b1419-320e-44e0-a6c2-823517cf07c7
keywords:
- RDBSS WDK ファイルシステム、名前キャッシュ
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、名前キャッシュ
- NAME_CACHE 構造体
- WDK RDBSS の名前
- WDK RDBSS をキャッシュする
- ファイルが見つからないことを確認するメッセージ WDK RDBSS
- 名前キャッシュ WDK RDBSS
- NAME_CACHE_CONTROL 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f960d927fe2c7cef915e555a6a5bc8ea6f334691
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841055"
---
# <a name="name-cache-management"></a>名前キャッシュ管理


## <span id="ddk_name_cache_management_if"></span><span id="DDK_NAME_CACHE_MANAGEMENT_IF"></span>


キャッシュ構造\_名前を指定すると、サーバーで実行された最近の操作の名前文字列がキャッシュされるため、クライアントは冗長な要求を抑制できます。 たとえば、開いている要求が最近失敗し、"ファイルが見つかりません" というメッセージが表示され、クライアントアプリケーションが大文字の文字列を使用して開いている要求を再度試行し、ネットワークミニリダイレクターが大文字と小文字を区別した名前をサポートしていない場合、RDBSS は要求を失敗させることができます。サーバーに到達することなくすぐに使用できます。

一般に、このアルゴリズムでは、名前\_キャッシュエントリに時間枠と操作数の制限を設定します。 通常、時間枠は2秒です。 そのため、NAME\_CACHE entry が2秒を超える場合、一致は失敗し、要求はサーバーに送られます。 サーバーで要求が再度失敗した場合は、\_キャッシュエントリの名前が、別の2秒のウィンドウで更新されます。 要求操作数が一致しない場合は、1つ以上の要求がサーバーに送信されています。これにより、この名前\_キャッシュエントリが無効になる可能性があります。 ここでも、この操作はサーバーに送信されます。

キャッシュ構造\_名前には、ネットワークミニリダイレクター、MRX\_NAME\_CACHE に公開されている部分と、RDBSS でのみ使用するプライベートセクションがあります。 ミニリダイレクターの部分には、この名前エントリに対する以前のサーバー操作の結果、および名前\_キャッシュと共同で割り当てることができる追加のミニリダイレクター固有のストレージ用のコンテキスト拡張機能ポインターのコンテキストフィールド NTSTATUS があります。データ. 詳細については、「 [**RxNameCacheInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize)」を参照してください。

Windows ネットワークの場合、SMB 操作数はミニリダイレクター固有の状態の例です。これは、MRX\_NAME\_CACHE のコンテキストフィールドに保存できます。 [**RxNameCacheCheckEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry)が呼び出されると、名前キャッシュ内の一致の検索の一部として、コンテキストフィールドと指定されたパラメーターの間で等価性のチェックが実行されます。 名前\_キャッシュエントリが作成または更新されると、このフィールドに適切な値を指定するためのネットワークミニリダイレクターのジョブと、NAME\_CACHE エントリの有効期間 (秒単位) が示されます。

名前\_キャッシュ構造体の private RDBSS 部分には、Unicode 文字列としての名前、高速参照を行う名前のハッシュ値、エントリの有効期限、およびサーバーが大文字と小文字を区別する名前をサポートするかどうかを示すフラグが含まれています。

\_制御構造の名前\_キャッシュは、特定の名前キャッシュを管理します。 これには、空きリスト、アクティブリスト、および更新を同期するためのロックがあります。 \_制御構造の名前\_キャッシュには、現在割り当てられている名前\_キャッシュエントリの数、割り当てられるエントリの最大数の値、使用される追加のネットワークミニリダイレクターストレージのサイズを格納するフィールドもあります。各名前\_キャッシュエントリ、統計の値 (キャッシュが更新された回数、確認された、有効な一致が返された回数、およびネットワークミニリダイレクターがネットワーク操作を保存した時刻)。 **Maximumentries**フィールドは、不適切なプログラムが大量のメモリを消費している不適切なファイル名を持つ多数のオープン要求を生成する場合に、作成されるキャッシュエントリ\_名前の数を制限します。

現在、オブジェクト\_名に対して RDBSS によって管理されている名前キャッシュが見つかりません\_\_。 この名前キャッシュでは、2秒のウィンドウが保持されます。これは、いずれかの操作がサーバーに送信されると無効になります。 これは、サーバー上のアプリケーションがサーバー上で別のファイル (サンプル 2) の作成を通知するために使用するファイル (サンプル 1) が開かれている場合に発生する可能性があります。 クライアントが最初のファイル (サンプル 1) を読み取って、2番目のファイル (サンプル 2) がサーバーに作成されたことを認識すると、2番目のファイル (サンプル 2) に一致する名前キャッシュのヒットがエラーを返すことはできません。 この最適化によって処理されるのは、まだ存在しない同じファイルに対して、連続したファイルのオープン操作が行われた場合のみです。 このシナリオは、Microsoft Word を使用して行われます。

RDBSS name キャッシュ管理ルーチンには、次のものが含まれます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheactivateentry" data-raw-source="[&lt;strong&gt;RxNameCacheActivateEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheactivateentry)"><strong>RxNameCacheActivateEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、名前キャッシュエントリを受け取り、有効期限とネットワークミニリダイレクターコンテキストを更新します。 次に、アクティブなリストにエントリを配置します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry" data-raw-source="[&lt;strong&gt;RxNameCacheCheckEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry)"><strong>RxNameCacheCheckEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリの有効性を確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecreateentry" data-raw-source="[&lt;strong&gt;RxNameCacheCreateEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecreateentry)"><strong>RxNameCacheCreateEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された名前の文字列を使用して NAME_CACHE 構造体を割り当て、初期化します。 呼び出し元は、name cache コンテキストの追加のネットワークミニリダイレクター要素を初期化し、そのエントリを name cache active list に配置する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentry" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentry)"><strong>RxNameCacheExpireEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリをフリーリストに挿入します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentrywithshortname" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntryWithShortName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentrywithshortname)"><strong>RxNameCacheExpireEntryWithShortName</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された短いファイル名と一致する名前プレフィックスを持つすべての NAME_CACHE エントリの有効期限が切れます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefetchentry" data-raw-source="[&lt;strong&gt;RxNameCacheFetchEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefetchentry)"><strong>RxNameCacheFetchEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリに対して指定された名前の文字列との一致を検索します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefinalize" data-raw-source="[&lt;strong&gt;RxNameCacheFinalize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefinalize)"><strong>RxNameCacheFinalize</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE_CONTROL 構造体に関連付けられているすべての NAME_CACHE エントリのストレージを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefreeentry" data-raw-source="[&lt;strong&gt;RxNameCacheFreeEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefreeentry)"><strong>RxNameCacheFreeEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリのストレージを解放し、NAME_CACHE_CONTROL 構造に関連付けられている NAME_CACHE キャッシュエントリの数を減らします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize" data-raw-source="[&lt;strong&gt;RxNameCacheInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize)"><strong>RxNameCacheInitialize</strong></a></p></td>
<td align="left"><p>このルーチンは、名前キャッシュ (NAME_CACHE_CONTROL 構造体) を初期化します。</p></td>
</tr>
</tbody>
</table>

 

 

 




