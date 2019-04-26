---
title: プレフィックス テーブル管理
description: プレフィックス テーブル管理
ms.assetid: a48ed460-fab9-4a6d-bd2f-454b4932ea61
keywords:
- RDBSS WDK ファイル システム、テーブルのプレフィックス
- リダイレクトされたバッファリング サブシステム WDK のドライブのファイル システム、テーブルのプレフィックス
- プレフィックス テーブル WDK ネットワーク リダイレクター
- WDK RDBSS 名
- バージョン スタンプ WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bea1f186462988c45a2c4eae99cce394e97b00bd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352896"
---
# <a name="prefix-table-management"></a>プレフィックス テーブル管理


## <span id="ddk_prefix_table_management_if"></span><span id="DDK_PREFIX_TABLE_MANAGEMENT_IF"></span>


RDBSS SRV カタログにテーブルをプレフィックスの使用を有効にするデータ構造を定義する\_呼び出し、NET\_ルート、および V\_NET\_ルート名。

RDBSS で名前の管理の現在の実装では、次のコンポーネントを持つテーブルを使用します。

-   挿入された名前のキュー

-   バージョン スタンプ

-   テーブルへのアクセスを制御するテーブルのロック リソース

-   名前の一致が大文字と小文字を区別しないかどうかを示す値

-   このプレフィックスのテーブルのハッシュ値のエントリのバケット

テーブルのロック リソースは、通常の方法で使用されます。 変更操作の排他的参照操作用に共有。

各変更でバージョン スタンプの変更。 キューの理由では、プレフィックスのテーブル パッケージで複数の呼び出し元はで列挙するのには、ことです。 挿入された名前とバージョン スタンプのキューでは、同時に列挙する複数の呼び出し元を許可します。 ファイル名に高速参照として、キューを使用できますが、プレフィックスのテーブルは、NET の適切なアプローチでは間違いなく\_ルート構造体。

これらのプレフィックス テーブル管理ルーチンはによって内部的に使用 RDBSS MUP からの呼び出しに応答で名前を要求するか、NET の作成のパスを形成する\_ルート構造体。 これら RDBSS プレフィックスにテーブルの管理テーブルにアクセスする前に適切なロックを獲得し、作業が完了したときに、ロックが解放限りも、ルーチンを使用してネットワークのミニ リダイレクターことができます。 ドライバーによっては、通常の使用であるようします。

-   共有ロックの取得を呼び出すことによって**RxAcquirePrefixTableLockShared**します。

-   呼び出すことによって、名前を調べる[ **RxPrefixTableLookupName**](https://msdn.microsoft.com/library/windows/hardware/ff554632)します。

-   呼び出すことによって、共有ロックを解放**RxReleasePrefixTableLock**します。

特定のルーチンが Windows XP と Windows の以前のバージョンでのみ実装されていることに注意してください。 [**RxPrefixTableLookupName** ](https://msdn.microsoft.com/library/windows/hardware/ff554632)は Windows のすべてのバージョンに実装されているプレフィックス テーブル管理ルーチンのみです

RDBSS プレフィックス テーブル管理ルーチンを以下に示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554595" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockExclusive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554595)"><strong>RxpAcquirePrefixTableLockExclusive</strong></a></p></td>
<td align="left"><p>このルーチンは、カタログ SRV_CALL と NET_ROOT 名に使用されるプレフィックス テーブルに対する排他ロックを取得します。</p>
<p>このルーチンは、Windows XP および Windows 2000 にできるだけです。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554598" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockShared&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554598)"><strong>RxpAcquirePrefixTableLockShared</strong></a></p></td>
<td align="left"><p>このルーチンは、カタログ SRV_CALL と NET_ROOT 名に使用されるプレフィックス テーブルに対する共有ロックを取得します。</p>
<p>このルーチンは、Windows XP および Windows 2000 にできるだけです。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554632" data-raw-source="[&lt;strong&gt;RxPrefixTableLookupName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554632)"><strong>RxPrefixTableLookupName</strong></a></p></td>
<td align="left"><p>ルーチンは、カタログ SRV_CALL に使用されるプレフィックスのテーブルの名前と NET_ROOT 名を検索し、基になるポインターから、包含構造体に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554637" data-raw-source="[&lt;strong&gt;RxpReleasePrefixTableLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554637)"><strong>RxpReleasePrefixTableLock</strong></a></p></td>
<td align="left"><p>このルーチンは、カタログ SRV_CALL と NET_ROOT 名に使用されるプレフィックス テーブルのロックを解放します。</p>
<p>このルーチンは、Windows XP および Windows 2000 にできるだけです。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
</tbody>
</table>

 

Windows Server 2003 以降を除く、ルーチンは、前の表で説明されている[ **RxPrefixTableLookupName**](https://msdn.microsoft.com/library/windows/hardware/ff554632)マクロは置き換えられます。次のマクロは、プレフィックスが少ないパラメーターを持つテーブル ルーチンを呼び出すことで定義されます。

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
<td align="left"><p><strong>RxAcquirePrefixTableLockExclusive</strong> (<em>TABLE</em>, <em>WAIT</em>)</p></td>
<td align="left"><p>このマクロでは、変更操作の排他モードでプレフィックス テーブル ロックを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxAcquirePrefixTableLockShared</strong> (<em>TABLE</em>, <em>WAIT</em>)</p></td>
<td align="left"><p>このマクロでは、共有モードの検索操作でプレフィックス テーブル ロックを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsPrefixTableLockAcquired</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックス テーブル ロックが排他的であるか、または共有モードで取得されたかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsPrefixTableLockExclusive</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックスのテーブル ロックを排他モードで取得されたかどうかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReleasePrefixTableLock</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックスのテーブル ロックを解放します。</p></td>
</tr>
</tbody>
</table>

 

 

 




