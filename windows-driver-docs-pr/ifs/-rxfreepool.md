---
title: '\_RxFreePool 関数'
description: '\_使用して割り当てられていたメモリを解放する RxFreePool \_RxAllocatePoolWithTag します。'
ms.assetid: 383deda9-6151-420b-afa9-445cd05e998b
keywords:
- インストール可能なファイル システム ドライバーの _RxFreePool 関数
topic_type:
- apiref
api_name:
- _RxFreePool
api_location:
- ntrxdef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b424acace9d2e59e0c910301e762aace1ed73a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553429"
---
# <a name="rxfreepool-function"></a>\_RxFreePool 関数


**\_RxFreePool**を使用して割り当てられていたメモリを解放 **\_RxAllocatePoolWithTag**します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID _RxFreePool(
   PVOID Buffer,
   PSZ   FileName,
   ULONG LineNumber
);
```

<a name="parameters"></a>パラメーター
----------

*バッファー*   
プールのメモリが解放されるバッファーへのポインター。

*ファイル名*   
メモリの割り当てが発生したソース ファイル名へのポインター。 このパラメーターは現在は使用されません。

*LineNumber*   
メモリの割り当てが発生したソース ファイル内の行番号。 このパラメーターは現在は使用されません。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

推奨されます、 **RxFreePool**このルーチンを直接使用する代わりにマクロが呼び出されます。 呼び出す製品版ビルドでこのマクロが定義されている**ExFreePool**します。

割り当てられたメモリ[  **\_RxAllocatePoolWithTag** ](-rxallocatepoolwithtag.md)を呼び出して解放する必要が **\_RxFreePool**します。

 **\_RxFreePool**ルーチンの呼び出し**ExFreePool**します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntrxdef.h (Ntrxdef.h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**\_RxAllocatePoolWithTag**](-rxallocatepoolwithtag.md)

[**\_RxCheckMemoryBlock**](-rxcheckmemoryblock.md)

 

 






