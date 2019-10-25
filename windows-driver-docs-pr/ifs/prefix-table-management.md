---
title: プレフィックステーブル管理
description: プレフィックステーブル管理
ms.assetid: a48ed460-fab9-4a6d-bd2f-454b4932ea61
keywords:
- RDBSS WDK ファイルシステム, プレフィックステーブル
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、プレフィックステーブル
- プレフィックステーブル WDK ネットワークリダイレクター
- WDK RDBSS の名前
- バージョンスタンプ WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42d6a1ea66d365dc6c0d2062cf324125a8b4fbd4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841027"
---
# <a name="prefix-table-management"></a>プレフィックステーブル管理


## <span id="ddk_prefix_table_management_if"></span><span id="DDK_PREFIX_TABLE_MANAGEMENT_IF"></span>


RDBSS では、プレフィックステーブルの使用を有効にするデータ構造を定義しています。これは、SRV\_呼び出し、NET\_ROOT、および V\_NET\_のルート名に使用できるようにします。

RDBSS での name management の現在の実装では、次のコンポーネントを含むテーブルが使用されます。

-   挿入された名前のキュー

-   バージョンスタンプ

-   テーブルへのアクセスを制御するテーブルロックリソース

-   名前の一致で大文字と小文字を区別するかどうかを示す値

-   このプレフィックステーブルのハッシュ値エントリのバケット

テーブルロックリソースは通常の方法で使用されます。これは、参照操作のための共有で、変更操作専用です。

各変更に合わせてバージョンスタンプが変更されます。 キューの理由は、プレフィックステーブルパッケージによって、複数の呼び出し元が一度に列挙できることです。 挿入された名前とバージョンスタンプのキューを使用すると、複数の呼び出し元を同時に列挙できます。 キューはファイル名の高速な参照として使用できますが、プレフィックステーブルは、NET\_のルート構造の正しいアプローチであることが確実です。

これらのプレフィックステーブル管理ルーチンは、MUP からの呼び出しに応答して RDBSS によって内部的に使用され、名前を要求したり、NET\_のルート構造の作成パスを形成したりします。 これらの RDBSS プレフィックステーブル管理ルーチンは、テーブルにアクセスする前に適切なロックが取得され、作業が完了したときにロックが解放される限り、ネットワークミニリダイレクターでも使用できます。 ドライバーによって通常使用されるのは、次のようになります。

-   **RxAcquirePrefixTableLockShared**を呼び出して、共有ロックを取得します。

-   [**RxPrefixTableLookupName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)を呼び出して名前を検索します。

-   **RxReleasePrefixTableLock**を呼び出して、共有ロックを解除します。

一部のルーチンは、Windows XP およびそれ以前のバージョンの Windows でのみ実装されていることに注意してください。 [**RxPrefixTableLookupName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)は、すべてのバージョンの Windows に実装されている唯一のプレフィックステーブル管理ルーチンです。

RDBSS prefix テーブル管理ルーチンには、次のものが含まれます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockexclusive" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockExclusive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockexclusive)"><strong>RxpAcquirePrefixTableLockExclusive</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL と NET_ROOT の名前をカタログ化するために使用されるプレフィックステーブルに対して排他ロックを取得します。</p>
<p>このルーチンは、Windows XP および Windows 2000 でのみ使用できます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockshared" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockShared&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockshared)"><strong>RxpAcquirePrefixTableLockShared</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL と NET_ROOT の名前のカタログ化に使用されるプレフィックステーブルに対して共有ロックを取得します。</p>
<p>このルーチンは、Windows XP および Windows 2000 でのみ使用できます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname" data-raw-source="[&lt;strong&gt;RxPrefixTableLookupName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)"><strong>RxPrefixTableLookupName</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL と NET_ROOT の名前をカタログ化するために使用されるプレフィックステーブル内の名前を検索し、基になるポインターから含んでいる構造体に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpreleaseprefixtablelock" data-raw-source="[&lt;strong&gt;RxpReleasePrefixTableLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpreleaseprefixtablelock)"><strong>RxpReleasePrefixTableLock</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL と NET_ROOT の名前をカタログ化するために使用されるプレフィックステーブルのロックを解放します。</p>
<p>このルーチンは、Windows XP および Windows 2000 でのみ使用できます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
</tbody>
</table>

 

Windows Server 2003 以降では、前の表に示されているルーチン ( [**RxPrefixTableLookupName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)を除く) がマクロに置き換えられています。次のマクロは、より少数のパラメーターでプレフィックステーブルルーチンを呼び出すように定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxAcquirePrefixTableLockExclusive</strong> (<em>テーブル</em>、<em>待機</em>)</p></td>
<td align="left"><p>このマクロは、変更操作のために、排他モードでプレフィックステーブルロックを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxAcquirePrefixTableLockShared</strong> (<em>テーブル</em>、<em>待機</em>)</p></td>
<td align="left"><p>このマクロは、参照操作のために、共有モードでプレフィックステーブルロックを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsPrefixTableLockAcquired</strong> (<em>テーブル</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックステーブルロックが排他的モードまたは共有モードのいずれかで取得されたかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsPrefixTableLockExclusive</strong> (<em>テーブル</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックステーブルロックが排他モードで取得されたかどうかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReleasePrefixTableLock</strong> (<em>テーブル</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックステーブルロックを解放します。</p></td>
</tr>
</tbody>
</table>

 

 

 




