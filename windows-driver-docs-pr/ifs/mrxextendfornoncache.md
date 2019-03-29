---
title: MRxExtendForNonCache ルーチン
description: MRxExtendForNonCache ルーチンは、キャッシュ マネージャーによって、ファイルがキャッシュされていないときに、ネットワークのミニ リダイレクターがファイルを拡張する要求を RDBSS によって呼び出されます。
ms.assetid: 80ec5142-7188-45ba-a1cb-73be99ce1ac4
keywords:
- MRxExtendForNonCache ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 883b4a9f2844232a854175c31c3b4cc3b5fa1d6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571328"
---
# <a name="mrxextendfornoncache-routine"></a>MRxExtendForNonCache ルーチン


*MRxExtendForNonCache*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)キャッシュ マネージャーによって、ファイルがキャッシュされていないときに、ネットワークのミニ リダイレクターがファイルを拡張することを要求します。

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

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

*pNewFileSize* \[in, out\]  
全体へのポインター\_新しいファイル サイズのバイト数を示す整数値。

*pNewAllocationSize* \[out\]  
全体へのポインター\_する場合、新しい割り当てを格納するための整数のサイズ[ **MRxExtendForCache** ](https://msdn.microsoft.com/library/windows/hardware/ff549878)を返します。

<a name="return-value"></a>戻り値
------------

*MRxExtendForNonCache*ステータスを返します\_成功または失敗した場合、エラー コードに成功しました。

<a name="remarks"></a>コメント
-------

*MRxExtendForNonCache*ハンドルはネットワーク I/O の非キャッシュのファイルを拡張する要求。

呼び出しの前に*MRxExtendForNonCache*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**LowIoContext.Operation** LOWIO に設定されている\_OP\_書き込み

**LowIoContext.ParamsFor.ReadWrite.Flags** 、LOWIO は\_READWRITEFLAG\_拡張\_FILESIZE ビットが設定

ファイルまたはディレクトリの情報をキャッシュするネットワーク ・ mini-リダイレクターは、ファイルを拡張するときにその情報をキャッシュを無効にする必要があります。

<a name="requirements"></a>必要条件
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
<td align="left">Mrx.h (Mrx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxAreFilesAliased**](https://msdn.microsoft.com/library/windows/hardware/ff549838)

[**MRxCleanupFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549841)

[**MRxCloseSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff549845)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://msdn.microsoft.com/library/windows/hardware/ff549871)

[**MRxDeallocateForFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549872)

[**MRxExtendForCache**](https://msdn.microsoft.com/library/windows/hardware/ff549878)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://msdn.microsoft.com/library/windows/hardware/ff550677)

[**MRxIsLockRealizable**](https://msdn.microsoft.com/library/windows/hardware/ff550691)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






