---
title: '\_RxAllocatePoolWithTag 関数'
description: '\_RxAllocatePoolWithTag は、メモリ trashing のインスタンスをキャッチするために使用できる、ブロックの先頭に4バイトのタグがあるプールからメモリを割り当てます。'
ms.assetid: 5e999d06-ebcf-433a-a714-f340a1c74be1
keywords:
- _RxAllocatePoolWithTag 関数のインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 3e769e9952757794394cf5e92861bdbba07c69b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841513"
---
# <a name="_rxallocatepoolwithtag-function"></a>\_RxAllocatePoolWithTag 関数


**\_RxAllocatePoolWithTag**は、メモリ trashing のインスタンスをキャッチするために使用できる、ブロックの先頭に4バイトのタグがあるプールからメモリを割り当てます。

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
割り当てられるプールの種類。 このパラメーターには、プール\_型の次の列挙値のいずれかを指定できます。

<a href="" id="nonpagedpool"></a>**NonPagedPool**  
非ページングは、任意の IRQL からアクセスできるシステムメモリを使用します。 **NonPagedPool**メモリは不足しているリソースであり、ドライバーは必要なときにのみ割り当てます。 システムで割り当てることができるのは、ページ\_サイズの倍数で**NonPagedPool**からページ\_サイズより大きいバッファーのみです。 ページ\_サイズより大きいバッファーの要求に対して、複数の非ページングメモリを\_サイズではありません。

<a href="" id="pagedpool"></a>**PagedPool**  
IRQL &lt; ディスパッチ\_レベルでのみ割り当ておよびアクセスできるページング可能なシステムメモリ。

 *サイズ*  
割り当てるメモリブロックのサイズ (バイト単位)。

*タグ*   
割り当てられたバッファーをマークするために使用される4バイトのタグ。 タグの使用方法の詳細については、「 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)」を参照してください。 タグ内の各文字の ASCII 値は、0 ~ 127 の範囲で指定する必要があります。

*ファイル名*   
メモリ割り当てが発生したソースファイル名へのポインター。 このパラメーターは現在使用されていません。

*LineNumber*   
メモリ割り当てが発生したソースファイル内の行番号。 このパラメーターは現在使用されていません。

<a name="return-value"></a>戻り値
------------

**RxAllocatePoolWithTag**は、要求を満たすために空きプール内のメモリが不足している場合に**NULL**を返します。 それ以外の場合、ルーチンは割り当てられたメモリへのポインターを返します。

<a name="remarks"></a>注釈
-------

このルーチンを直接使用するのではなく、 **RxAllocatePoolWithTag**マクロを呼び出すことをお勧めします。 リテールビルドでは、このマクロは[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出すように定義されています。 チェックを行ったビルドでは、このマクロは **\_RxAllocatePoolWithTag**を呼び出すように定義されています。

**\_RxAllocatePoolWithTag**ルーチンは、lowpoolpriority に設定された優先度 (要求の重要度) を使用して**Exallocatepoolwithtagpriority**を呼び出します。 リソースが不足している場合、システムは LowPoolPriority の要求に失敗する可能性があります。 このルーチンを使用する場合は、ドライバーを割り当てエラーから回復するように準備する必要があります。

システムがページの\_サイズ以上のプールメモリからバッファーを割り当てた場合、バッファーはページの境界に配置されます。 ページ\_サイズより小さいメモリ要求は、必ずしもページの境界に沿って配置されるわけではありませんが、常に1つのページに収まるように、8バイトの境界に合わせて配置されます。 ページサイズの倍数ではないブロックを要求する正常に割り当てられた場合は、最後に割り当てられたページの未使用のバイトがすべて無駄になります。これは、ページ\_サイズの倍数ではない\_ブロックを要求します。

システムは、割り当てられたメモリに pool タグを関連付けます。 WinDbg などのプログラミングツールでは、割り当てられた各バッファーに関連付けられたプールタグを表示できます。 *タグ*の値は通常、逆順で表示されます。 たとえば、呼び出し元が "Fred" を*タグ*として渡すと、メモリがダンプされた場合、またはデバッガーのメモリ使用量を追跡している場合は、' derf ' として表示されます。

**\_RxAllocatePoolWithTag**で割り当てられたメモリは[ **\_RxFreePool**](-rxfreepool.md)を呼び出すことによって解放する必要があります。

**\_RxAllocatePoolWithTag**の呼び出し元は、IRQL &lt;= ディスパッチ\_レベルで実行されている必要があります。 ディスパッチ\_レベルで実行している呼び出し元は、*型*パラメーターに**NonPagedPool**値を指定する必要があります。 IRQL &lt;= APC\_LEVEL で実行される呼び出し元は、*型*パラメーターに任意のプール\_型の値を指定できます。

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
<td align="left">Ntrxdef. h (Ntrxdef. h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>「解説」を参照してください。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**Exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

[ **\_RxCheckMemoryBlock**](-rxcheckmemoryblock.md)

[ **\_RxFreePool**](-rxfreepool.md)

 

 






