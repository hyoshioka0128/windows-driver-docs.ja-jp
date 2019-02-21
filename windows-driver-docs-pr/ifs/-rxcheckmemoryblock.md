---
title: '\_RxCheckMemoryBlock ルーチン'
description: '\_RxCheckMemoryBlock メモリ ブロックを特別な RX チェック\_プール\_ヘッダー ヘッダーの署名。'
ms.assetid: 972cef55-e541-450c-8128-1d026042c4ca
keywords:
- _RxCheckMemoryBlock ルーチン インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- _RxCheckMemoryBlock
api_location:
- ntrxdef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03bbc59aa34dfce4503f4b7fe17e04a2ac0c29bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550903"
---
# <a name="rxcheckmemoryblock-routine"></a>\_RxCheckMemoryBlock ルーチン


**\_RxCheckMemoryBlock**メモリ ブロックを特別な RX チェック\_プール\_ヘッダー ヘッダーの署名。 ルーチンを使用するには、ネットワークのミニ リダイレクター ドライバーはメモリにこの特別な署名ブロックを追加する必要がありますので注意が割り当てられます。 この特殊なヘッダー ブロックが実装されていないために、このルーチンを使用しない必要があります。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
BOOLEAN _RxCheckMemoryBlock(
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
メモリの割り当てが発生したソース ファイル名へのポインター。

*LineNumber*   
メモリの割り当てが発生したソース ファイル内の行番号。

<a name="return-value"></a>戻り値
------------

**RxCheckMemoryBlock**返します**TRUE**メモリ ブロックは、チェックをパスした場合または**FALSE**失敗した場合。

<a name="remarks"></a>注釈
-------

推奨されます、 **RxCheckMemoryBlock**このルーチンを直接使用する代わりにマクロが呼び出されます。 製品版ビルドでは、このマクロに何も定義されます。 呼び出すチェック済みのビルドでこのマクロが定義されている **\_RxCheckMemoryBlock**します。

このルーチンは、特殊なメモリのヘッダー ブロックからは使用できません (RX\_プール\_ヘッダー) を呼び出すときに、このルーチンをチェックしない追加、  **\_RxAllocatePoolWithTag**ルーチン。 ネットワークのミニ リダイレクター ドライバーは、このルーチンを使用するために割り当てられたメモリへのこの特殊な署名ブロックを追加する必要があります。

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

[**\_RxFreePool**](-rxfreepool.md)

 

 






