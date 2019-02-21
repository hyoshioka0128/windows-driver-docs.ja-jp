---
title: poolfind
description: Poolfind 拡張機能は、いずれかの非ページまたはページ メモリ プール内の特定のプール タグのすべてのインスタンスを検索します。
ms.assetid: 01783b6b-0117-49ca-87ca-bbe3c1b0e730
keywords:
- Windows デバッグ poolfind
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolfind
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b774ea44405fe0208fc293369f48ff56f2a370fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558515"
---
# <a name="poolfind"></a>! poolfind


**! Poolfind**拡張機能は、いずれかの非ページまたはページのメモリ プール内で特定のプール タグのすべてのインスタンスを検索します。

```dbgcmd
!poolfind TagString [PoolType] 
!poolfind TagValue [PoolType] 
```

## <a name="span-idddkpoolfinddbgspanspan-idddkpoolfinddbgspanparameters"></a><span id="ddk__poolfind_dbg"></span><span id="DDK__POOLFIND_DBG"></span>パラメーター


<span id="_______TagString______"></span><span id="_______tagstring______"></span><span id="_______TAGSTRING______"></span> *TagString*   
プール タグを指定します。 *TagString*大文字の ASCII 文字列です。 アスタリスク (\*) 任意の文字数を表すために使用することができます。 1 文字を表すために使用する、疑問符 (?) は。 アスタリスクを使用すると、しない限り、 *TagString*に 4 文字の長さでなければなりません。

<span id="_______TagValue______"></span><span id="_______tagvalue______"></span><span id="_______TAGVALUE______"></span> *TagValue*   
プール タグを指定します。 *TagValue*場合でも、既定の基数は 16 に、"0 x"で始まる必要があります。 このパラメーターは、その他の値 (「0 X」を含む) で始まるタグ ASCII 文字列として解釈されます。

<span id="_______PoolType______"></span><span id="_______pooltype______"></span><span id="_______POOLTYPE______"></span> *PoolType*   
検索対象のプールの種類を指定します。 次の値が許可されています。

<span id="0"></span>0  
非ページ メモリ プールを指定します。 これが既定値です。

<span id="1"></span>1  
ページ メモリ プールを指定します。

<span id="2"></span>2  
特別なプールを指定します。

<span id="4"></span>4  
セッションのプールを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

メモリ プールおよびプール タグについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

このコマンドは、検索する必要がありますプール メモリのサイズによっては、実行に時間のかなり時間がかかることができます。 この実行の速度で COM ポートの速度が向上、 [ **CTRL + A (トグル ボー レート)** ](ctrl-a--toggle-baud-rate-.md)キー、またはを使用して、 [ **.cache (キャッシュ サイズを設定する)** ](-cache--set-cache-size-.md)(約 10 MB) にキャッシュ サイズを大きくコマンド。

プール タグに渡された同じタグ、**ExAllocate * * * Xxx*ルーチンのファミリです。

次に例を示します。 全体の非ページ プールの検索しページ プールは、検索しますが、(操作の 1 時間) の後に完了する前に、コマンドが終了しました。

```dbgcmd
kd> !poolfind SeSd 0

Scanning large pool allocation table for Tag: SeSd (827d1000 : 827e9000)

Searching NonPaged pool (823b1000 : 82800000) for Tag: SeSd

826fa130 size:   c0 previous size:   40  (Allocated) SeSd
82712000 size:   c0 previous size:    0  (Allocated) SeSd
82715940 size:   a0 previous size:   60  (Allocated) SeSd
8271da30 size:   c0 previous size:   10  (Allocated) SeSd
82721c00 size:   10 previous size:   30  (Free)      SeSd
8272b3f0 size:   60 previous size:   30  (Allocated) SeSd
8272d770 size:   60 previous size:   40  (Allocated) SeSd
8272d7d0 size:   a0 previous size:   60  (Allocated) SeSd
8272d960 size:   a0 previous size:   70  (Allocated) SeSd
82736f30 size:   a0 previous size:   10  (Allocated) SeSd
82763840 size:   a0 previous size:   10  (Allocated) SeSd
8278b730 size:  100 previous size:  290  (Allocated) SeSd
8278b830 size:   10 previous size:  100  (Free)      SeSd
82790130 size:   a0 previous size:   20  (Allocated) SeSd
82799180 size:   a0 previous size:   10  (Allocated) SeSd
827c00e0 size:   a0 previous size:   30  (Allocated) SeSd
827c8320 size:   a0 previous size:   60  (Allocated) SeSd
827ca180 size:   a0 previous size:   50  (Allocated) SeSd
827ec140 size:   a0 previous size:   10  (Allocated) SeSd

Searching NonPaged pool (fe7c3000 : ffbe0000) for Tag: SeSd

kd> !poolfind SeSd 1

Scanning large pool allocation table for Tag: SeSd (827d1000 : 827e9000)

Searching Paged pool (e1000000 : e4400000) for Tag: SeSd

e10000b0 size:   d0 previous size:   20  (Allocated) SeSd
e1000260 size:   d0 previous size:   60  (Allocated) SeSd
......
e1221dc0 size:   a0 previous size:   60  (Allocated) SeSd
e1224250 size:   a0 previous size:   30  (Allocated) SeSd

...terminating - searched pool to e1224000
kd> 
```

 

 





