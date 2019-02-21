---
title: プールのタグ付けを有効にします。
description: プールのタグ付けを有効にします。
ms.assetid: e88f97a0-a8c3-4162-871a-b78671b902bb
keywords:
- プールのタグ (グローバル フラグ) を有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dabbd77f722b6d6b55c0062b42487ea6432a08d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537400"
---
# <a name="enable-pool-tagging"></a>プールのタグ付けを有効にします。


## <span id="ddk_enable_pool_tagging_dtools"></span><span id="DDK_ENABLE_POOL_TAGGING_DTOOLS"></span>


**プール タグ付けを有効にする**フラグは、データを収集し、プール タグ値で並べ替えられたプールのメモリ割り当てに関する統計を計算します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>ptg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x400</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_POOL_ENABLE_TAGGING</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>変換先</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

このフラグは、Windows Server 2003 以降のバージョンの Windows で完全に設定されます。 これらのシステムで、**プール タグ付けを有効にする** ダイアログ ボックスでグローバル フラグのチェック ボックスが淡色表示され、有効または無効にするためのコマンドは、タグ付けの失敗をプールします。

使用**exallocatepoolwithtag に**または**ExAllocatePoolWithQuotaTag**タグ値を設定します。 タグの値が指定されていない場合 (**ExAllocatePool**、 **ExAllocatePoolWithQuota**)、Windows で、既定値は"None"のタグを作成します。 すべての割り当てを"None"タグを組み合わせると、データを識別できないため、特定の割り当てのデータ。 これらのルーチンの詳細については、Windows Driver Kit (WDK) を参照してください。

Windows XP およびそれ以前のシステムでは、このフラグも指示を使用してプールのメモリが割り当てられている場合でも、プール タグをアタッチする Windows **ExAllocatePoolWithQuotaTag**します。 それ以外の場合、タグのバイトを使用してクォータ値を格納します。 Windows Server 2003 では、タグの値とクォータの値は、各プールのメモリ割り当てに関連付けられている個別のフィールドに格納されます。

**注**   Windows でのタグが付けられた割り当てについて収集されるデータを表示するには、PoolMon、Windows Driver Kit に含まれているツールを使用します。
説明、**プールのタグ付けを有効にする**フラグは、Windows XP サポート ツールのドキュメントが完了していません。 このフラグは、Windows の収集し、タグ値でデータを処理するよう指示します。

 

 

 





