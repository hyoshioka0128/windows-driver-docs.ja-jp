---
title: PoolMon を使用したカーネルモード メモリ リークの検出
description: PoolMon を使用したカーネルモード メモリ リークの検出
ms.assetid: 383b5d9a-3e99-4dc5-bce9-bd44f2ef1dc0
keywords:
- メモリ リークが発生する場合、カーネル モードの PoolMon
- PoolMon
- PoolMon、メモリ リークを検出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 848b8e11bcd03bfa26161ff814dd034b3ffe8951
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381019"
---
# <a name="using-poolmon-to-find-a-kernel-mode-memory-leak"></a>PoolMon を使用したカーネルモード メモリ リークの検出


カーネル モードのメモリ リークがあると思われる場合、どのプール タグがリークに関連付けを判断する最も簡単な方法は PoolMon ツールを使用するは。

PoolMon (Poolmon.exe) のモニターは、プール タグ名でメモリ使用量をプールします。 このツールは、Windows Driver Kit (WDK) で含まれています。 詳細については、次を参照してください。 [PoolMon](https://go.microsoft.com/fwlink/p/?linkid=122776) WDK ドキュメント。

### <a name="span-idenablepooltaggingwindows2000andwindowsxpspanspan-idenablepooltaggingwindows2000andwindowsxpspanenable-pool-tagging-windows-2000-and-windows-xp"></a><span id="enable_pool_tagging__windows_2000_and_windows_xp_"></span><span id="ENABLE_POOL_TAGGING__WINDOWS_2000_AND_WINDOWS_XP_"></span>プール (Windows 2000 および Windows XP) のタグ付けを有効にします。

Windows 2000 および Windows XP では、GFlags を使用してプールのタグ付けを有効にする必要があります。 Windows ツールをデバッグには GFlags が含まれます。 開始 GFlags、選択、**システム レジストリ** タブで、チェック、**プールのタグ付けを有効にする**ボックスをクリックして**適用**します。 この設定を有効にする Windows を再起動する必要があります。 詳細については、次を参照してください。 [GFlags](gflags.md)します。

Windows Server 2003 および Windows の以降のバージョンでは、プールのタグ付けは常に有効です。

### <a name="span-idusingpoolmonspanspan-idusingpoolmonspanusing-poolmon"></a><span id="using_poolmon"></span><span id="USING_POOLMON"></span>PoolMon を使用します。

PoolMon ヘッダーには、ページ合計と非ページ プールのバイト数が表示されます。 列は、各プール タグのプールの使用を示しています。 表示が数秒ごとに自動的に更新します。 次に、例を示します。

```dbgcmd
Memory: 16224K Avail: 4564K PageFlts: 31 InRam Krnl: 684K P: 680K
Commit: 24140K Limit: 24952K Peak: 24932K Pool N: 744K P: 2180K

## Tag   Type  Allocs       Frees        Diff    Bytes       Per Alloc


CM    Paged   1283  ( 0)  1002  ( 0)   281  1377312   ( 0)  4901
Strg  Paged  10385 ( 10)  6658  ( 4)  3727   317952 ( 512)    85
Fat   Paged   6662  ( 8)  4971  ( 6)  1691   174560 ( 128)   103
MmSt  Paged    614  ( 0)   441  ( 0)   173    83456   ( 0)   482 
```

PoolMon では、さまざまな条件に従って出力を並べ替えるコマンド キーがあります。 再度データを並べ替えるために各コマンドに関連付けられている文字を押します。 各コマンドを実行するのに数秒をかかります。

並べ替えコマンドは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド キー</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>P</strong></p></td>
<td align="left"><p>非ページ プール、ページ プール、またはその両方に表示されているタグを制限します。 繰り返し押すと<strong>P</strong>の順序で各オプションを切り替えます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>最大バイトを使用してタグを並べ替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>M</strong></p></td>
<td align="left"><p>タグの最大バイト割り当てによって並べ替えます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>T</strong></p></td>
<td align="left"><p>タグをタグ名のアルファベット順に並べ替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>E</strong></p></td>
<td align="left"><p>ページおよび非ページ合計が下部に表示をによりします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>A</strong></p></td>
<td align="left"><p>タグの割り当てのサイズによって並べ替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>F</strong></p></td>
<td align="left"><p>無料の操作でタグを並べ替えます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>S</strong></p></td>
<td align="left"><p>タグの割り当ての違いによって並べ替え、解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Q</strong></p></td>
<td align="left"><p>PoolMon を終了します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idusingthepoolmonutilitytofindamemoryleakspanspan-idusingthepoolmonutilitytofindamemoryleakspanusing-the-poolmon-utility-to-find-a-memory-leak"></a><span id="using_the_poolmon_utility_to_find_a_memory_leak"></span><span id="USING_THE_POOLMON_UTILITY_TO_FIND_A_MEMORY_LEAK"></span>PoolMon ユーティリティを使用してメモリ リークの検出

PoolMon ユーティリティを使用したメモリ リークを検索するには、この手順に従います。

1.  PoolMon を開始します。

2.  非ページ プールのリークが発生していることを決定した場合、以下のキーを押して**P**ページ プールで発生していることを決定した場合を押して 1 回; **P** 2 回です。 不明な場合を押さない**P**とプールの両方の種類が含まれています。

3.  キーを押して**B**最大バイトを使用して、表示の並べ替えにします。

4.  テストを開始します。 スクリーン ショットをとって、メモ帳にコピーします。

5.  30 分ごとにショット新しい画面を取得します。 スクリーン ショットを比較すると、特定するタグのバイト数が増加します。

6.  テストを停止し、いくつかの時間待機します。 タグの量が解放この時間内か。

通常、アプリケーションには、安定性が実行状態に達すると、割り当てますメモリとほぼ同じ速度で空きメモリ。 メモリの割り当てが解放されますよりも高速化する傾向が場合、は、メモリ使用量が時間の経過と共に拡張されます。 これにより、メモリ リークが多くの場合を示します。

### <a name="span-idaddressingtheleakspanspan-idaddressingtheleakspanaddressing-the-leak"></a><span id="addressing_the_leak"></span><span id="ADDRESSING_THE_LEAK"></span>メモリ リークをアドレス指定

どのプール タグは、リークに関連付けが決まったら、これは、リークについて知っておく必要がありますすべてを表示する可能性があります。 必要がある場合は、ルーチンを決定する特定のインスタンス、割り当てのメモリ リークの原因となってを参照してください[カーネル モード メモリ リークの検出にカーネル デバッガーを使用して](using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak.md)します。

 

 





