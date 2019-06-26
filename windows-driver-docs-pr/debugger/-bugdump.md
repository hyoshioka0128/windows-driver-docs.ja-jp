---
title: bugdump
description: Bugdump 拡張機能では、書式設定し、バグ チェック コールバック バッファーに含まれる情報を表示します。
ms.assetid: cbea92de-e45b-416c-87f1-6faba95788d0
keywords:
- Windows デバッグ bugdump
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bugdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 84f5a2916529f95aaa945dbce03bc9e10555067f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363171"
---
# <a name="bugdump"></a>!bugdump


**! Bugdump**拡張機能のフォーマットし、バグ チェック コールバック バッファーに含まれている情報が表示されます。

```dbgsyntax
    !bugdump [Component] 
```

## <a name="span-idddkbugdumpdbgspanspan-idddkbugdumpdbgspanparameters"></a><span id="ddk__bugdump_dbg"></span><span id="DDK__BUGDUMP_DBG"></span>パラメーター


<span id="_______Component______"></span><span id="_______component______"></span><span id="_______COMPONENT______"></span> *コンポーネント*   
コールバック データを調査するが、コンポーネントを指定します。 省略した場合、すべてのバグ チェック コールバック データが表示されます。

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

詳細については、次を参照してください。[バグ チェック コールバックのデータの読み取り](reading-bug-check-callback-data.md)します。

<a name="remarks"></a>注釈
-------

この拡張機能は、バグ チェックが行われた後、またはカーネル モードのクラッシュ ダンプ ファイルをデバッグするときにのみ使用できます。

*コンポーネント*パラメーターで使用される最後のパラメーターに対応[ **KeRegisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckcallback)します。

最小メモリ ダンプには、コールバックのデータを保持するバッファーを使用できません。 これらのバッファーは、カーネル メモリ ダンプし、完全メモリ ダンプに存在します。 ただし、Windows XP SP1、Windows Server 2003、および以降のバージョンの Windows、ダンプ ファイルが作成されるドライバーの前に**BugCheckCallback**ルーチンが呼び出され、そのため、これらのバッファーにはこれらによって書き込まれたデータは含まないルーチン。

クラッシュしたシステムのライブ デバッグを実行する場合は、すべてのコールバック データが表示されます。

 

 





