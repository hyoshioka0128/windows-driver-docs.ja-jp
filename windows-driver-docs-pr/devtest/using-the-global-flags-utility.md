---
title: グローバル フラグ ユーティリティの使用
description: グローバル フラグ ユーティリティの使用
ms.assetid: 934272e9-867c-4eb4-8bc1-e65e5b3f2aeb
keywords:
- グローバル フラグ ユーティリティ
- Driver Verifier の WDK、グローバル フラグ ユーティリティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97aefe3397738391d7c510d92aa7028917a2c1b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579460"
---
# <a name="using-the-global-flags-utility"></a>グローバル フラグ ユーティリティの使用


## <span id="ddk_using_the_global_flags_utility_tools"></span><span id="DDK_USING_THE_GLOBAL_FLAGS_UTILITY_TOOLS"></span>


グローバル フラグ (gflags.exe) ユーティリティでは、システム レジストリ内の特定のキーの設定、実行中のシステムのカーネル設定を調整すること、およびイメージ ファイルの設定を変更することの簡単な方法を提供します。 これらのキーは、グラフィカルまたはコマンド ライン インターフェイスを使用して設定できます。

Windows サポート ツール パッケージとツールを Windows のデバッグ パッケージは、グローバル フラグ ユーティリティを確認できます。 後者については、[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)を参照してください。

グローバル フラグ ユーティリティは、ドライバーの検証ツールの特別なプールのオプションを構成するか、個々 のメモリ割り当てに使用するための特別なプールを指定するにも使用できます。

特別なプールの設定を変更するには、グローバル フラグ開始ユーティリティと選択、**システム レジストリ**内のオプション ボタン、**先**セクション。 **カーネル特別なプール タグ** ダイアログ ボックスのセクションでは特定の特別なプールのオプションを設定します。

### <a name="span-idcontrollingpooltagalignmentspanspan-idcontrollingpooltagalignmentspancontrolling-pool-tag-alignment"></a><span id="controlling_pool_tag_alignment"></span><span id="CONTROLLING_POOL_TAG_ALIGNMENT"></span>プール タグのアラインメントを制御します。

選択、**確認を開始**させるアンダーラン検出に集中する特別なプールの配置オプション ボタンをクリックします。 選択、**終了の確認**オーバーランの検出に集中するオプション。 これらのボタンは、Driver Verifier またはグローバル フラグによって行われたかどうか、--すべての特別なプールの割り当ての配置を制御します。

### <a name="span-idusingspecialpoolbypooltagorallocationsizespanspan-idusingspecialpoolbypooltagorallocationsizespanusing-special-pool-by-pool-tag-or-allocation-size"></a><span id="using_special_pool_by_pool_tag_or_allocation_size"></span><span id="USING_SPECIAL_POOL_BY_POOL_TAG_OR_ALLOCATION_SIZE"></span>プールでプールの特殊なタグまたは割り当てサイズを使用してください。

特別なプールを特定のプール タグを持つすべての割り当てに使用できます。 この機能をアクティブ化するにプール タグを入力、**プール タグ**テキスト ボックス。

特別なプールは、特定のサイズの範囲内のすべての割り当てにも使用できます。 この機能がそれでもに数値を入力してアクティブ化されるが、この特別なプールの使用は、プール タグを含まない、**プール タグ**テキスト ボックス。 この番号はページ未満である必要があります\_サイズ。

X86 プロセッサでは、ページ\_サイズは、0x1000、割り当てサイズの範囲が 8 バイトの長さ。 特別なプールのサイズがこの範囲内のすべての割り当てをアクティブ化するには、この範囲と 8 の最大値に等しい数値を入力します。 (この数は常に 8 の倍数) です。次の表は、これらの値を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サイズの範囲</th>
<th align="left">プール タグのテキスト ボックスにこの番号を入力します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 から 8 バイト</p></td>
<td align="left"><p>16 (0x10)</p></td>
</tr>
<tr class="even">
<td align="left"><p>9 ~ 16 バイト</p></td>
<td align="left"><p>24 (0x18)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>17 ~ 24 バイト</p></td>
<td align="left"><p>32 (0x20)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFE9 に 0xFF0 バイト</p></td>
<td align="left"><p>0xFF8</p></td>
</tr>
</tbody>
</table>

 

X64 のプロセッサ、ページ\_サイズは、0x1000、割り当てサイズの範囲が 16 バイトの長さ。 特別なプールのサイズがこの範囲内のすべての割り当てをアクティブ化するには、この範囲と 16 の最大値に等しい数値を入力します。 (この数は常に 16 の倍数) です。次の表は、これらの値を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サイズの範囲</th>
<th align="left">プール タグのテキスト ボックスにこの番号を入力します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 ~ 16 バイト</p></td>
<td align="left"><p>32 (0x20)</p></td>
</tr>
<tr class="even">
<td align="left"><p>17 ~ 32 バイト</p></td>
<td align="left"><p>48 (0x30)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33 ~ 48 バイト</p></td>
<td align="left"><p>64 (0x40)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFD1 に 0xFE0 バイト</p></td>
<td align="left"><p>0xFF0</p></td>
</tr>
</tbody>
</table>

 

ページ、itanium プロセッサ\_サイズは 0x2000、割り当てサイズの範囲が 16 バイトの長さ。 特別なプールのサイズがこの範囲内のすべての割り当てをアクティブ化するには、この範囲と 16 の最大値に等しい数値を入力します。 (この数は常に 16 の倍数) です。次の表は、これらの値を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サイズの範囲</th>
<th align="left">プール タグのテキスト ボックスにこの番号を入力します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 ~ 16 バイト</p></td>
<td align="left"><p>32 (0x20)</p></td>
</tr>
<tr class="even">
<td align="left"><p>17 ~ 32 バイト</p></td>
<td align="left"><p>48 (0x30)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33 ~ 48 バイト</p></td>
<td align="left"><p>64 (0x40)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1FD1 に 0x1FE0 バイト</p></td>
<td align="left"><p>0x1FF0</p></td>
</tr>
</tbody>
</table>

 

ページよりも低いプール タグの使用を回避することをお勧め\_サイズ。 たとえば、0x30 を Itanium ベースのプロセッサでこのテキスト ボックスに配置した場合特別なプールは 17 と 32 バイトとの間のすべての割り当てを使用 0x0030 プール タグの割り当て。

**注**   Driver Verifier の特別なドライバーのプールが有効にし、グローバル フラグ ユーティリティがプール タグまたは割り当てのサイズの特別なプールを有効に場合これらの条件 (のいずれかを満たすすべての割り当ての特別なプールが使用されますプール可能な場合)。

 

参照してください[特別なプール](special-pool.md)特別なプールの使用方法の詳細。

 

 





