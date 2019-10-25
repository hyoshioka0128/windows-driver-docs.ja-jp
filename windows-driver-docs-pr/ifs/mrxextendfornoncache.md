---
title: MRxExtendForNonCache ルーチン
description: MRxExtendForNonCache ルーチンは、ファイルがキャッシュマネージャーによってキャッシュされていない場合に、ネットワークミニリダイレクターがファイルを拡張するよう要求するために、RDBSS によって呼び出されます。
ms.assetid: 80ec5142-7188-45ba-a1cb-73be99ce1ac4
keywords:
- MRxExtendForNonCache ルーチンのインストール可能なファイルシステムドライバー
- PMRX_EXTENDFILE_CALLDOWN
topic_type:
- apiref
api_name:
- MRxExtendForNonCache
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a04795dd28991dbff6802a7976dada38d8f42420
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841111"
---
# <a name="mrxextendfornoncache-routine"></a>MRxExtendForNonCache ルーチン


*MRxExtendForNonCache*ルーチンは、ファイルがキャッシュマネージャーによってキャッシュされていない場合に、ネットワークミニリダイレクターがファイルを拡張するよう要求するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_EXTENDFILE_CALLDOWN MRxExtendForNonCache;

ULONG MRxExtendForNonCache(
  _Inout_ PRX_CONTEXT    RxContext,
  _Inout_ PLARGE_INTEGER pNewFileSize,
  _Out_   PLARGE_INTEGER pNewAllocationSize
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

*Pnewfilesize サイズ*の \[in、out\]  
新しいファイルサイズのバイト数を示す大きな\_整数値へのポインター。

*Pnewのサイズ*\[out\]  
[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)が返されたときに、新しい割り当てサイズを格納するための大きな\_整数へのポインター。

<a name="return-value"></a>戻り値
------------

*MRxExtendForNonCache*は、成功した場合は状態\_成功した場合は、失敗した場合はエラーコードを返します。

<a name="remarks"></a>注釈
-------

*MRxExtendForNonCache*は、キャッシュされていない i/o 用にファイルを拡張するネットワーク要求を処理します。

*MRxExtendForNonCache*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**Lowiocontext。操作**は LOWIO\_OP\_WRITE に設定されています

**Lowiocontext** . READWRITEFLAG には、\_の\_のビットセットを拡張する LOWIO\_があります

ファイルまたはディレクトリの情報をキャッシュするネットワークミニリダイレクターは、ファイルが拡張されるときに、キャッシュ情報を無効にすることが必要になる場合があります。

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
<td align="left">Mrx .h (Mrx を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxAreFilesAliased**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






