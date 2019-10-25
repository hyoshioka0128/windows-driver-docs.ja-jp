---
title: カーネルモードドライバーが開始した IRP_MJ_CREATE 操作に ECPs をアタッチします。
description: カーネルモードドライバーが開始した IRP_MJ_CREATE 操作に ECPs をアタッチする
ms.assetid: 87daa861-b0d5-4877-bf16-fad120108de6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 229ecc8cfbf0f7c6b661ce6222dee804a9e72356
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841488"
---
# <a name="attaching-ecps-to-irp_mj_create-operations-that-a-kernel-mode-driver-originated"></a>カーネルモードドライバーが開始する操作を作成するために ECPs を IRP\_MJ にアタッチ\_


次の手順に従って、ECPs を設定し、ファイルに対する[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作に接続する必要があります。

1.  [**FltAllocateExtraCreateParameterList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterlist)または[**FsRtlAllocateExtraCreateParameterList**](https://msdn.microsoft.com/library/windows/hardware/ff545632)ルーチンを呼び出して、 [ECP\_LIST](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体にメモリを割り当てます。 オペレーティングシステムは、ECP\_リストの構造を自動的に解放しません。 その代わりに、ECP\_リスト構造が割り当てられた後、ミニフィルタードライバーは、 [**FltFreeExtraCreateParameterList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist)または[**FsRtlFreeExtraCreateParameterList**](https://msdn.microsoft.com/library/windows/hardware/ff546005)ルーチンを呼び出して、ecp\_リストを解放する必要があります。

2.  [**FltAllocateExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter)または[**FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)ルーチンを呼び出して、ECP コンテキスト構造にページングされたメモリプールを割り当て、その構造体へのポインターを生成します。

3.  [**FltInsertExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter)または[**FsRtlInsertExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546179)ルーチンを呼び出して、ecp のコンテキスト構造を[ecp\_LIST](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体に挿入します。

4.  [**IoInitializeDriverCreateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioinitializedrivercreatecontext)ルーチンを呼び出して、 [ **\_コンテキスト構造を作成\_IO\_ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)を初期化します。

5.  [ **\_コンテキスト構造\_作成する IO\_ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)を定義します。 この定義では、 **IO\_ドライバー**の**ExtraCreateParameter**メンバーをポイントし\_、\_コンテキストを[ECP\_リスト](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造に作成します。

6.  [**FltCreateFileEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefileex2)または[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)ルーチンを呼び出して、ファイルの[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作に ecps をアタッチします。 この呼び出しで、 [**i/o\_ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)へのポインターを渡し、 *drivercontext*パラメーターに\_コンテキスト構造を作成\_ます。

7.  [**FltFreeExtraCreateParameterList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist)または[**FsRtlFreeExtraCreateParameterList**](https://msdn.microsoft.com/library/windows/hardware/ff546005)ルーチンを呼び出して、 [ECP\_リスト](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))の構造を解放します。

 

 




