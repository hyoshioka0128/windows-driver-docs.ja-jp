---
title: バグダンプ
description: バグダンプ拡張機能は、バグチェックコールバックバッファーに格納されている情報を書式設定して表示します。
ms.assetid: cbea92de-e45b-416c-87f1-6faba95788d0
keywords:
- Windows デバッグのバグダンプ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bugdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ca89bba30361213d77ecc6a788a985eb6dc4b62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837606"
---
# <a name="bugdump"></a>!bugdump


**! Bug dump**拡張機能は、バグチェックコールバックバッファーに格納されている情報を書式設定して表示します。

```dbgsyntax
    !bugdump [Component] 
```

## <a name="span-idddk__bugdump_dbgspanspan-idddk__bugdump_dbgspanparameters"></a><span id="ddk__bugdump_dbg"></span><span id="DDK__BUGDUMP_DBG"></span>パラメータ


<span id="_______Component______"></span><span id="_______component______"></span><span id="_______COMPONENT______"></span>*コンポーネント*の   
コールバックデータを検査するコンポーネントを指定します。 省略した場合、すべてのバグチェックコールバックデータが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、「[バグチェックのコールバックデータの読み取り](reading-bug-check-callback-data.md)」を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能は、バグチェックが発生した後、またはカーネルモードのクラッシュダンプファイルをデバッグしている場合にのみ使用できます。

*Component*パラメーターは、 [**KeRegisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckcallback)で使用される最後のパラメーターに対応します。

コールバックデータを保持するバッファーは、小さいメモリダンプでは使用できません。 これらのバッファーは、カーネルメモリダンプとフルメモリダンプに存在します。 ただし、Windows XP SP1、Windows Server 2003、およびそれ以降のバージョンの Windows では、ドライバーの**バグチェックコールバック**ルーチンが呼び出される前にダンプファイルが作成されるため、これらのバッファーにはこれらのルーチンによって書き込まれたデータが含まれません。

クラッシュしたシステムのライブデバッグを実行している場合は、すべてのコールバックデータが表示されます。

 

 





