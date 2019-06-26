---
title: ルック アサイド
description: ルック アサイドの拡張機能は、ルック アサイド リストに関する情報が表示されます、ルック アサイド リストのカウンターをリセットします。 または、ルック アサイド リストの深さを変更します。
ms.assetid: ec343563-f293-4ddf-96c8-69fc7b9b4377
keywords:
- ルック アサイド リスト
- ルック アサイドの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lookaside
api_location:
- Kdexts.dll
api_type:
- DllExport
ms.localizationpriority: medium
ms.openlocfilehash: a94732fc070f29d09aa343e8ad31f54fe53af299
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365792"
---
# <a name="lookaside"></a>!lookaside


**! ルック アサイド**拡張子ルック アサイド リストに関する情報が表示されます、ルック アサイド リストのカウンターをリセットまたはルック アサイド リストの深さを変更します。

```dbgcmd
!lookaside [Address [Options [Depth]]]
!lookaside [-all]
!lookaside 0 [-all]
```

## <a name="span-idddklookasidedbgspanspan-idddklookasidedbgspanparameters"></a><span id="ddk__lookaside_dbg"></span><span id="DDK__LOOKASIDE_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ルック アサイド リストを表示または変更の 16 進数のアドレスを指定します。

場合*アドレス*を省略すると (または 0) および **-すべて**オプションが指定されていない、よく知られている、標準のシステムのルック アサイド リストのセットが表示されます。 リストのセットはすべてを網羅します。つまり、すべてのシステムのルック アサイド リストは含まれません。 また、セットにはカスタム ルック アサイド リストへの呼び出しによって作成された含まれません[ **ExInitializePagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)または[ **ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist).

場合*アドレス*を省略すると (または 0) および **-すべて**オプションを指定すると、すべてのルック アサイド リストが表示されます。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
どのような操作が実行を制御します。 次の考えられる*オプション*はサポートされています。 既定値は、0 です。

<span id="0"></span>0  
指定されたルック アサイド リストまたはリストに関する情報が表示されます。

<span id="1"></span>1  
指定されたルック アサイド リストのカウンターをリセットします。

<span id="2"></span>2  
指定されたルック アサイド リストの深さを変更します。 このオプションは、場合にのみ使用できます*アドレス*が 0 以外。

<span id="_______Depth______"></span><span id="_______depth______"></span><span id="_______DEPTH______"></span> *深さ*   
指定されたルック アサイド リストの新しい最大の深さを指定します。 場合にのみ、このパラメーターは許可されて*アドレス*が 0 以外と*オプション*が 2 と等しい。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ルック アサイド リストについては、次を参照してください。、 [Windows Driver Kit (WDK) ドキュメント](https://go.microsoft.com/fwlink/p/?linkid=201141)と*Microsoft Windows internals 』* 、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>コメント
-------

ルック アサイド リストは、ページ、または非ページ メモリからエントリの固定サイズのプールを管理するためのマルチプロセッサの安全なメカニズムです。

ルック アサイド リストは、ルーチンはほとんどのプラットフォームでスピン ロックを使用しないため、効率的です。

ルック アサイド リストの現在の深さがそのリストに関連付けられている構造体を解放し、そのリストの最大の深さを超えた場合と、メモリの一覧表示ではなく、プールのメモリに解放することに注意してください。

この拡張機能からの出力の例を次に示します。

```dbgcmd
!lookaside 0xfffff88001294f80

Lookaside "" @ 0xfffff88001294f80  Tag(hex): 0x7366744e "Ntfs"
    Type           =       0011  PagedPool RaiseIfAllocationFailure
    Current Depth  =          0  Max Depth  =          4
    Size           =        496  Max Alloc  =       1984
    AllocateMisses =          8  FreeMisses =          0
    TotalAllocates =     272492  TotalFrees =     272488
    Hit Rate       =         99% Hit Rate   =        100%
```

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Kdexts.dll</td>
</tr>
</tbody>
</table>

 

 





