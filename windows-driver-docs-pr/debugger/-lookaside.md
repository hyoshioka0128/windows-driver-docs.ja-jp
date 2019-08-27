---
title: ルック
description: ルックアサイドの拡張機能では、ルックアップリストに関する情報が表示されます。また、ルックアサイドリストのカウンターがリセットされます。または、ルックアップリストの深さが変更されます。
ms.assetid: ec343563-f293-4ddf-96c8-69fc7b9b4377
keywords:
- ルックアサイドリスト
- ルックアサイド Windows デバッグ
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
ms.openlocfilehash: 6bd117702ffff4e3124ea83a884397b65d9f4dac
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025223"
---
# <a name="lookaside"></a>!lookaside


**! ルックアサイド**拡張機能では、ルックアップリストに関する情報が表示されます。また、ルックアサイドリストのカウンターがリセットされます。または、ルックアップリストの深さが変更されます。

```dbgcmd
!lookaside [Address [Options [Depth]]]
!lookaside [-all]
!lookaside 0 [-all]
```

## <a name="span-idddk__lookaside_dbgspanspan-idddk__lookaside_dbgspanparameters"></a><span id="ddk__lookaside_dbg"></span><span id="DDK__LOOKASIDE_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
表示または変更するルックアップリストの16進数のアドレスを指定します。

*Address*が省略されている場合 (または 0)、 **-all**オプションが指定されていない場合は、既知の標準システムのルックアップリストが表示されます。 リストのセットは完全ではありません。つまり、すべてのシステムのルックアップリストが含まれているわけではありません。 また、このセットには、 [**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)または[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)の呼び出しによって作成されたカスタムのルックアサイドリストは含まれません。

*Address*が省略されている場合 (または 0)、 **-all**オプションが指定されている場合は、すべてのルックアップリストが表示されます。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
実行する操作を制御します。 次の*オプション*がサポートされています。 既定値は0です。

<span id="0"></span>0  
指定したルックアップリストまたはリストに関する情報を表示します。

<span id="1"></span>1  
指定したルックアップリストのカウンターをリセットします。

<span id="2"></span>3  
指定したルックアップリストの深さを変更します。 このオプションは、*アドレス*が0以外の場合にのみ使用できます。

<span id="_______Depth______"></span><span id="_______depth______"></span><span id="_______DEPTH______"></span>*深さ*   
指定された検索除外リストの新しい最大深度を指定します。 このパラメーターは、 *Address*が0以外で、*オプション*が2に等しい場合にのみ許可されます。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ルックアサイドリストの詳細については、「 [Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=201141) 」のドキュメントと*Microsoft windows の内部*(Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

ルックアサイドリストは、ページ分割されたメモリまたはページングされていないメモリの固定サイズのエントリのプールを管理するためのマルチプロセッサセーフメカニズムです。

ルーチンではほとんどのプラットフォームでスピンロックが使用されないため、ルックアサイドリストは効率的です。

検索対象リストの現在の深さがそのリストの最大深度を超える場合、そのリストに関連付けられている構造体を解放すると、リストメモリではなくプールメモリに解放されることに注意してください。

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
<td align="left">Kdexts .dll</td>
</tr>
</tbody>
</table>

 

 





