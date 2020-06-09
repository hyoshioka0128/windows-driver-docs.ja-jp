---
title: PoolMon を使用したカーネルモード メモリ リークの検出
description: PoolMon を使用したカーネルモード メモリ リークの検出
ms.assetid: 383b5d9a-3e99-4dc5-bce9-bd44f2ef1dc0
keywords:
- メモリリーク、カーネルモード、PoolMon
- PoolMon
- PoolMon、メモリリークの検出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6487d067042aab9835519579fdf0b552f566f1b
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534751"
---
# <a name="using-poolmon-to-find-a-kernel-mode-memory-leak"></a>PoolMon を使用したカーネルモード メモリ リークの検出


カーネルモードのメモリリークが発生していると思われる場合は、どのプールタグがリークに関連付けられているかを判断する最も簡単な方法は、PoolMon ツールを使用することです。

PoolMon (Poolmon) は、プールのメモリ使用量をプールタグ名で監視します。 このツールは、Windows Driver Kit (WDK) に含まれています。 詳細については、WDK ドキュメントの「 [PoolMon](https://docs.microsoft.com/windows-hardware/drivers/devtest/poolmon) 」を参照してください。

### <a name="span-idenable_pool_tagging__windows_2000_and_windows_xp_spanspan-idenable_pool_tagging__windows_2000_and_windows_xp_spanenable-pool-tagging-windows-2000-and-windows-xp"></a><span id="enable_pool_tagging__windows_2000_and_windows_xp_"></span><span id="ENABLE_POOL_TAGGING__WINDOWS_2000_AND_WINDOWS_XP_"></span>プールのタグ付けを有効にする (Windows 2000 および Windows XP)

Windows 2000 および Windows XP では、最初に GFlags を使用してプールのタグ付けを有効にする必要があります。 GFlags は、Windows 用デバッグツールに含まれています。 GFlags を起動し、[**システムレジストリ**] タブを選択し、[**プールタグ付けを有効にする**] チェックボックスをオンにして、[**適用**] をクリックします。 この設定を有効にするには、Windows を再起動する必要があります。 詳細については、「 [GFlags](gflags.md)」を参照してください。

Windows Server 2003 以降のバージョンの Windows では、プールのタグ付けは常に有効になっています。

### <a name="span-idusing_poolmonspanspan-idusing_poolmonspanusing-poolmon"></a><span id="using_poolmon"></span><span id="USING_POOLMON"></span>PoolMon の使用

PoolMon ヘッダーには、ページプールおよび非ページプールの合計バイト数が表示されます。 列には、プールタグごとにプールの使用が表示されます。 表示は、数秒ごとに自動的に更新されます。 次に例を示します。

```dbgcmd
Memory: 16224K Avail: 4564K PageFlts: 31 InRam Krnl: 684K P: 680K
Commit: 24140K Limit: 24952K Peak: 24932K Pool N: 744K P: 2180K

## Tag   Type  Allocs       Frees        Diff    Bytes       Per Alloc


CM    Paged   1283  ( 0)  1002  ( 0)   281  1377312   ( 0)  4901
Strg  Paged  10385 ( 10)  6658  ( 4)  3727   317952 ( 512)    85
Fat   Paged   6662  ( 8)  4971  ( 6)  1691   174560 ( 128)   103
MmSt  Paged    614  ( 0)   441  ( 0)   173    83456   ( 0)   482 
```

PoolMon には、さまざまな条件に従って出力を並べ替えるコマンドキーがあります。 データを並べ替えるには、各コマンドに関連付けられている文字を押します。 各コマンドが動作するまで数秒かかります。

並べ替えコマンドには次のものがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンドキー</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>P</strong></p></td>
<td align="left"><p>非ページプール、ページプール、またはその両方に表示されるタグを制限します。 <strong>P</strong>キーを繰り返し押すと、これらの各オプションが順番に切り替わります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>最大バイト使用率でタグを並べ替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>M</strong></p></td>
<td align="left"><p>最大バイト割り当てでタグを並べ替えます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>T</strong></p></td>
<td align="left"><p>タグ名のアルファベット順にタグを並べ替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>E</strong></p></td>
<td align="left"><p>表示に、ページングされた合計とページングされていない合計を下に含めます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>A</strong></p></td>
<td align="left"><p>割り当てサイズでタグを並べ替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>F</strong></p></td>
<td align="left"><p>自由操作でタグを並べ替えます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>2$s</strong></p></td>
<td align="left"><p>割り当てと解放の違いによってタグを並べ替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Q.</strong></p></td>
<td align="left"><p>PoolMon を終了します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idusing_the_poolmon_utility_to_find_a_memory_leakspanspan-idusing_the_poolmon_utility_to_find_a_memory_leakspanusing-the-poolmon-utility-to-find-a-memory-leak"></a><span id="using_the_poolmon_utility_to_find_a_memory_leak"></span><span id="USING_THE_POOLMON_UTILITY_TO_FIND_A_MEMORY_LEAK"></span>PoolMon ユーティリティを使用してメモリリークを検出する

PoolMon ユーティリティを使用してメモリリークを検出するには、次の手順に従います。

1.  PoolMon を開始します。

2.  ページングされていないプールでリークが発生していると判断した場合は、 **P**キーを1回押します。ページプールで発生していると判断した場合は、 **P**キーを2回押します。 わからない場合は、 **P**を押さないでください。両方の種類のプールが含まれています。

3.  **B**キーを押して、表示を最大バイト数で並べ替えます。

4.  テストを開始します。 スクリーンショットを取り、メモ帳にコピーします。

5.  30分ごとに新しいスクリーンショットを撮影します。 スクリーンショットを比較することで、増加しているタグのバイト数を特定します。

6.  テストを停止し、数時間待機します。 この時間内に解放されたタグの量を確認できます。

通常、アプリケーションは安定した実行状態に達すると、メモリとメモリをほぼ同じ速度で割り当てます。 メモリが解放されるよりも高速にメモリが割り当てられる傾向がある場合は、メモリの使用量が時間の経過と共に増加します。 これは多くの場合、メモリリークを示しています。

### <a name="span-idaddressing_the_leakspanspan-idaddressing_the_leakspanaddressing-the-leak"></a><span id="addressing_the_leak"></span><span id="ADDRESSING_THE_LEAK"></span>リークに対処する

リークに関連付けられているプールタグを特定した後で、リークについて知る必要があることが明らかになる可能性があります。 リークの原因となっている割り当てルーチンのインスタンスを特定する必要がある場合は、「カーネル[デバッガーを使用してカーネルモードのメモリリークを検出](using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak.md)する」を参照してください。

 

 





