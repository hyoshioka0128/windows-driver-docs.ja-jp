---
title: システム領域メモリの割り当て
description: システム領域メモリの割り当て
ms.assetid: eee425b3-6ddd-4e9d-b51d-1f2c9ea106a5
keywords:
- メモリ管理 WDK カーネル、システムによって割り当てられた領域
- システムによって割り当てられた領域 (WDK カーネル)
- システム領域メモリの割り当て
- i/o バッファーメモリの割り当て
- I/o バッファーメモリ割り当て (WDK カーネル)
- バッファーメモリ割り当て (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f00fcdad9405abf62c25c522b25a6586be03d1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837234"
---
# <a name="allocating-system-space-memory"></a>システム領域メモリの割り当て





ドライバーは、デバイスの[拡張機能](device-extensions.md)内のシステム割り当て領域を、デバイス固有の情報のグローバルストレージ領域として使用できます。 ドライバーは、カーネルスタックのみを使用して、少量のデータを内部ルーチンに渡すことができます。 一部のドライバーでは、多くの場合、i/o バッファー用に追加の大量のシステム領域メモリを割り当てる必要があります。

I/o バッファー領域を割り当てるには、使用する最適なメモリ割り当てルーチンは、 [**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)、 [**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)、 [**allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer) (ドライバーのデバイスでバスマスタ dma またはシステム dma コントローラーの自動初期化モードが使用されている場合)、または[**exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)です。

通常、非ページプールはシステムの実行中に断片化されます。そのため、ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、これらのルーチンを呼び出して、ドライバーが必要とするすべての長期的な i/o バッファーを設定する必要があります。 これらの各ルーチン ( [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を除く) は、最適なパフォーマンスを提供するために、プロセッサ固有の境界 (プロセッサのデータキャッシュラインサイズによって決まります) にアラインされたメモリを割り当てます。

非ページプールメモリはシステムリソースが限られているので、ドライバーは可能な限り経済的に i/o バッファーを割り当てる必要があります。 通常、ドライバーでは、これらのサポートルーチンを繰り返し呼び出して、ページ\_サイズ未満の割り当てを要求することを回避する必要があります。これは、ページ\_サイズより小さい割り当てにも、割り当てを内部で管理するために使用されるプールヘッダーが付属しているためです。

### <a name="tips-for-allocating-driver-buffer-space-economically"></a>ドライバーのバッファー領域を経済的に割り当てるためのヒント

I/o バッファーメモリを経済的に割り当てるには、次の点に注意してください。

-   [**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)または[**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)を呼び出すたびに、システムのページサイズの倍数が、要求された割り当てのサイズに関係なく、システムのページサイズの非ページシステムメモリの完全な倍数で返されます。 したがって、ページより小さい要求ではページ数がいっぱいになり、ページの残りのバイトは無駄になります。関数を呼び出したドライバーからはアクセスできません。また、他のカーネルモードコードでは使用できません。

-   [**Allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)を呼び出すたびに、少なくとも1つのバイトと1つのページをマップする、少なくとも1つのアダプターオブジェクトマップレジスタが使用されます。 マップレジスタと一般的なバッファーの使用の詳細については、「[アダプタオブジェクトと DMA](adapter-objects-and-dma.md)」を参照してください。

### <a name="allocating-memory-with-exallocatepoolwithtag"></a>ExAllocatePoolWithTag を使用したメモリの割り当て

また、ドライバーは、次のシステム定義のプールのいずれかを指定して、 *Pooltype*パラメーターの[ **\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)の値を指定して、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出すこともできます。

-   *Pooltype* = 、ドライバーが IRQL &gt; APC\_レベルで実行されているときに、ドライバーがアクセスする可能性のある、デバイス拡張機能またはコントローラー拡張機能に格納されていないすべてのオブジェクトまたはリソースに対して**NonPagedPool**です。

    この*Pooltype*値の場合、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)は、指定された*NUMBEROFBYTES*がページ\_サイズ以下である場合に要求されるメモリ量を割り当てます。 それ以外の場合、最後に割り当てられたページの残りのバイトは無駄になります。呼び出し元はアクセスできず、他のカーネルモードコードでは使用できません。

    たとえば、x86 では、割り当て要求が5キロバイト (KB) の場合、4 KB のページが2つ返されます。 2番目のページの最後の 3 KB は、呼び出し元または別の呼び出し元には使用できません。 非ページプールを無駄にしないように、ドライバーは複数のページを効率的に割り当てる必要があります。 この場合、たとえば、ドライバーは2つの割り当てを行うことができます。1つはページ\_サイズ用で、もう1つは 1 KB です。これにより、合計 5 KB が割り当てられます。

    **注**  Windows Vista 以降では、2つの割り当てが不要になるように、システムによって追加のメモリが自動的に追加されます。

     

-   *Pooltype* = 、IRQL &lt;= APC\_レベルで常にアクセスされ、ファイルシステムの書き込みパスにはないメモリの**PagedPool**です。

要求されたバイト数を割り当てることができない場合、 **Exallocatepoolwithtag**は**NULL**ポインターを返します。 ドライバーは、返されたポインターを常に確認する必要があります。 値が**NULL**の場合、 **driverentry**ルーチン (または、NTSTATUS 値を返すその他のドライバールーチン) は、不足している\_リソース\_不足しているか、可能であればエラー状態を処理する必要があります。

 

 




