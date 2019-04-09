---
title: vprot
description: Vprot 拡張機能には、仮想メモリの保護の情報が表示されます。
ms.assetid: 7ee863ef-abfd-4ee7-9bac-34472e60f3fa
keywords:
- メモリ、メモリの保護
- Windows デバッグ vprot
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vprot
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b361b4e7c5c9c384c7310cba599acde22419e52
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238527"
---
# <a name="vprot"></a>!vprot


**! Vprot**拡張機能には、仮想メモリの保護の情報が表示されます。

```dbgcmd
!vprot [Address]
```

## <a name="span-idddkvprotdbgspanspan-idddkvprotdbgspanparameters"></a><span id="ddk__vprot_dbg"></span><span id="DDK__VPROT_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
メモリ保護状態が表示される 16 進数のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Uext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ターゲット プロセスが所有するすべてのメモリの範囲のメモリ保護情報を表示する使用[ **! vadump**](-vadump.md)します。 メモリ保護については、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

**! Vprot**ライブ デバッグ ダンプ ファイルのデバッグと拡張機能のコマンドを使用できます。

以下に例を示します。

```dbgcmd
0:000> !vprot 30c191c
BaseAddress: 030c1000
AllocationBase: 030c0000
AllocationProtect: 00000080 PAGE_EXECUTE_WRITECOPY
RegionSize: 00011000
State: 00001000 MEM_COMMIT
Protect: 00000010 PAGE_EXECUTE
Type: 01000000 MEM_IMAGE
```

この表示では、AllocationProtect 線は、既定の保護に対しとリージョン全体が作成されたことを示します。 このリージョン内で個々 のアドレスでメモリが割り当てられた後に変更される、保護を使用できることに注意してください (場合など、 **VirtualProtect**と呼びます)。 保護する行は、この特定のアドレスの実際の保護を示しています。 保護可能な値はページ\_NOACCESS、ページ\_READONLY、ページ\_READWRITE、ページ\_EXECUTE、ページ\_EXECUTE\_読み取り、ページ\_EXECUTE\_READWRITE、ページ\_WRITECOPY、ページ\_EXECUTE\_WRITECOPY、およびページ\_ガード。

状態の行に渡される特定の仮想アドレスにも適用されます **! vprot**します。 可能な状態値はメモリ最適化\_コミット、メモリ最適化\_無償商品、およびメモリ最適化\_予約します。

型の行では、メモリの種類を示します。 使用可能な値はメモリ最適化\_イメージ、メモリ最適化\_マップ済み、およびメモリ最適化\_プライベートです。

 

 





