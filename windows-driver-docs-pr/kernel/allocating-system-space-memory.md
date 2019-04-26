---
title: システム領域メモリの割り当て
description: システム領域メモリの割り当て
ms.assetid: eee425b3-6ddd-4e9d-b51d-1f2c9ea106a5
keywords:
- メモリ管理の WDK カーネル、システムによって割り当てられた領域
- システムによって割り当てられた領域の WDK カーネル
- システム容量のメモリの割り当てください。
- I/O バッファー メモリの割り当て
- I/O バッファーのメモリ割り当ての WDK カーネル
- バッファー メモリの割り当ての WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9dc9dfcf7f903ac0dc34adfdae9b6bdc3888f0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348563"
---
# <a name="allocating-system-space-memory"></a>システム領域メモリの割り当て





ドライバー内でシステムによって割り当てられた領域を使用できます、[デバイス拡張機能](device-extensions.md)としてデバイスに固有の情報のグローバル ストレージ領域。 ドライバーは、カーネル スタックのみを使用して、その内部のルーチンに少量のデータを渡します。 一部のドライバーは、I/O バッファーの通常システム容量のメモリ量が、追加の拡大を割り当てる必要です。

使用する最適なメモリ割り当てルーチンには I/O バッファーの容量の割り当て、 [ **MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479)、 [ **MmAllocateContiguousMemorySpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554464)、 [ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575) (かどうか、ドライバーのデバイスではバス マスター DMA またはシステム DMA コント ローラーの自動初期化モード)、または[ **Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)します。

システムを実行すると、そのために、非ページ プールが通常断片化がドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンは、ドライバーを長期的な I/O バッファーを設定するこれらのルーチンを呼び出す必要があります必要があります。 これらのルーチンの各を除く[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)最高を提供 (プロセッサのキャッシュ ラインのデータのサイズによって決まります) プロセッサに固有の境界に配置されるメモリを割り当てますパフォーマンス。

ドライバーは、非ページ プール メモリが限られたシステム リソースであるために、I/O バッファーをできるだけ経済的割り当てる必要があります。 通常、ドライバーがこれらの呼び出しを回避する必要がありますページ未満の割り当てを要求するには、繰り返しのルーチンをサポートして\_ため各割り当てページよりも小さい\_サイズに内部的に使用するプールのヘッダーも付属しています割り当てを管理します。

### <a name="tips-for-allocating-driver-buffer-space-economically"></a>経済的ドライバー バッファー領域を割り当てるためのヒント

経済的な I/O バッファーのメモリを割り当てに、次の注意。

-   呼び出しごとに[ **MmAllocateNonCachedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554479)または[ **MmAllocateContiguousMemorySpecifyCache** ](https://msdn.microsoft.com/library/windows/hardware/ff554464)の完全な倍数は常に返しますシステムの非ページ システム領域のメモリ、要求された割り当てのサイズはどのようなページ サイズ。 そのため、完全なページとページの残りの部分 (バイト) が無駄になります。 ページが最大に丸められますよりも少ないの要求します。これらは、関数を呼び出すし、他のカーネル モード コードでは使用できませんが、ドライバーによってアクセスできません。

-   呼び出しごとに[ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575)少なくとも 1 バイト、最大で 1 つのページにマップするには少なくとも 1 つのアダプター オブジェクト マップ レジスタ使用します。 マップの詳細についてを登録し、一般的なバッファーを使用して、参照してください[アダプター オブジェクトと DMA](adapter-objects-and-dma.md)します。

### <a name="allocating-memory-with-exallocatepoolwithtag"></a>Exallocatepoolwithtag とメモリの割り当てください。

ドライバーを呼び出すことも[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)、システム定義の次のいずれかを示す[**プール\_型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)の値を*PoolType*パラメーター。

-   *PoolType* = **NonPagedPool**オブジェクト、またはデバイスの拡張機能または IRQL での実行中に、ドライバーにアクセスするコント ローラー拡張機能に格納されていないリソース&gt;APC\_レベル。

    この*PoolType*値、 [ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)場合に要求したメモリを割り当てて、指定した*NumberOfBytes*がページに小さい\_サイズ。 最後に割り当てられたページの残りの部分 (バイト) が浪費され、それ以外の場合: 呼び出し元にアクセスできないと他のカーネル モード コードで使用できなくなります。

    たとえば、x86、5 キロバイト (KB) の割り当て要求に 2 つの 4 KB のページが返されます。 2 番目のページの最後の 3 KB では、呼び出し元または他の呼び出し元を使用できません。 非ページ プールの浪費を回避するには、は、ドライバーが、複数のページを効率的に割り当てる必要があります。 この場合、たとえば、ドライバーは、ページに 1 つずつ、2 つの割り当て\_サイズおよびその他、1 KB の文字数は 5 KB を割り当てます。

    **注**  以降 Windows Vista では、自動的に追加されます追加のメモリのため、2 つの割り当てが必要ではありません。

     

-   *PoolType* = **プール**IRQL で常にアクセスされるメモリの&lt;APC を =\_レベルが、ファイル システムの書き込みパスにないとします。

**Exallocatepoolwithtag に**を返します、 **NULL**ポインターの場合は、要求されたバイト数を割り当てることができません。 ドライバーでは、返されたポインターを常に確認する必要があります。 その値が場合**NULL**、 **DriverEntry**ルーチン (または NTSTATUS 値を返す他のドライバー ルーチン) は、状態を返す必要があります\_不十分\_リソースまたはハンドル、エラー状態で可能な場合。

 

 




