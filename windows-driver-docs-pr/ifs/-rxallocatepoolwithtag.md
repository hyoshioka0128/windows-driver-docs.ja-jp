---
title: '\_RxAllocatePoolWithTag 関数'
description: '\_RxAllocatePoolWithTag は、メモリの破壊のインスタンスを検出するときに使用できるブロックの先頭 4 バイトのタグを使用して、プールからメモリを割り当てます。'
ms.assetid: 5e999d06-ebcf-433a-a714-f340a1c74be1
keywords:
- インストール可能なファイル システム ドライバーの _RxAllocatePoolWithTag 関数
topic_type:
- apiref
api_name:
- _RxAllocatePoolWithTag
api_location:
- ntrxdef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1b804bf7f2fd8cd580827f6a54df0bef192a20c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344594"
---
# <a name="rxallocatepoolwithtag-function"></a>\_RxAllocatePoolWithTag 関数


**\_RxAllocatePoolWithTag**メモリの破壊のインスタンスを検出するときに使用できるブロックの先頭 4 バイトのタグを使用して、プールからメモリを割り当てます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID* _RxAllocatePoolWithTag(
   ULONG Type,
   ULONG Size,
   ULONG Tag,
   PSZ   FileName,
   ULONG LineNumber
);
```

<a name="parameters"></a>パラメーター
----------

*型*   
プールが割り当てられるの型。 このパラメーターは、プールの列挙値は次のいずれかを指定できます\_型。

<a href="" id="nonpagedpool"></a>**NonPagedPool**  
IRQL からアクセスできる非ページ システム メモリです。 **NonPagedPool**メモリが不足しているリソースであり、ドライバーには、必要な場合にのみ割り当てる必要があります。 システムは、ページよりも大きいバッファーを割り当てることができますのみ\_からサイズ**NonPagedPool**ページの倍数で\_サイズ。 ページよりも大きいバッファーに対する要求\_、サイズがページではなく\_複数のサイズを非ページング メモリを無駄にします。

<a href="" id="pagedpool"></a>**PagedPool**  
ページング可能なシステム メモリを割り当てられたし、IRQL でアクセスできるだけ&lt;ディスパッチ\_レベル。

*サイズ*   
割り当てるバイトで、メモリ ブロックのサイズ。

*タグ*   
割り当てられたバッファーをマークするために使用する 4 バイト タグ。 タグを使用する方法については、次を参照してください。 [ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)します。 タグ内の各文字の ASCII 値は 0 ~ 127 の範囲にある必要があります。

*ファイル名*   
メモリの割り当てが発生したソース ファイル名へのポインター。 このパラメーターは現在は使用されません。

*LineNumber*   
メモリの割り当てが発生したソース ファイル内の行番号。 このパラメーターは現在は使用されません。

<a name="return-value"></a>戻り値
------------

**RxAllocatePoolWithTag**返します**NULL**要求を満たすための空きプールに十分なメモリがある場合。 それ以外の場合、ルーチンは、割り当てられたメモリへのポインターを返します。

<a name="remarks"></a>注釈
-------

推奨されます、 **RxAllocatePoolWithTag**このルーチンを直接使用する代わりにマクロが呼び出されます。 呼び出す製品版ビルドでこのマクロが定義されている[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)します。 呼び出すチェック済みのビルドでこのマクロが定義されている **\_RxAllocatePoolWithTag**します。

 **\_RxAllocatePoolWithTag**ルーチンの呼び出し**ExAllocatePoolWithTagPriority** LowPoolPriority に設定された優先順位 (要求の重要度) にします。 システムは、リソースの少ない実行時に、LowPoolPriority の要求は失敗します。 このルーチンを使用する場合、割り当てエラーから回復するには、ドライバーを準備する必要があります。

ときに、システムがページのメモリをプールからバッファーを割り当てます\_サイズ以上、バッファー ページ境界に合わせて配置します。 メモリの要求ページよりも小さい\_サイズは必ずしもページの境界にアラインされますが、常に 1 つのページに収まるし、は、8 バイト境界にアラインされます。 ページを超えるブロックを要求するすべての成功した割り当て\_ページの倍数でないサイズ\_サイズが最後に割り当てられたページで使用されていないすべてのバイトを浪費します。

システムでは、割り当てられたメモリをプール タグを関連付けます。 プログラミング、WinDbg などのツールと、割り当てられた各バッファーに関連付けられたプール タグを表示できます。 値*タグ*通常逆の順序で表示します。 たとえば、呼び出し元は 'Fred' として渡します、*タグ*、メモリ ダンプの場合、またはデバッガーのメモリ使用量を追跡する場合は 'derF' として表示されます。

割り当てられたメモリ **\_RxAllocatePoolWithTag**を呼び出して解放する必要が[  **\_RxFreePool**](-rxfreepool.md)します。

呼び出し元 **\_RxAllocatePoolWithTag** IRQL で実行する必要があります&lt;= ディスパッチ\_レベル。 ディスパッチを実行して呼び出し元\_レベルを指定する必要があります、 **NonPagedPool**値、*型*パラメーター。 IRQL でを実行する呼び出し元&lt;APC を =\_レベルは、すべてのプールを指定できます\_の型の値、*型*パラメーター。

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
<td align="left"><p>「解説」セクションをご覧ください。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)

[**\_RxCheckMemoryBlock**](-rxcheckmemoryblock.md)

[**\_RxFreePool**](-rxfreepool.md)

 

 






