---
title: カーネル モード ドライバーで発生した irp_mj_create 用 Operations に ECPs をアタッチします。
description: カーネルモード ドライバーが開始した IRP_MJ_CREATE 操作に ECP をアタッチする
ms.assetid: 87daa861-b0d5-4877-bf16-fad120108de6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47446a0bbe085f18e9ec9ce816d12f96b6a39e2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385323"
---
# <a name="attaching-ecps-to-irpmjcreate-operations-that-a-kernel-mode-driver-originated"></a>IRP への ECPs\_MJ\_作成操作、カーネル モード ドライバーで発生しました。


次の手順を実行 ECPs を設定する ECPs をアタッチする必要があります、 [ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)ファイルの操作。

1.  呼び出す、 [ **FltAllocateExtraCreateParameterList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocateextracreateparameterlist)または[ **FsRtlAllocateExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff545632)メモリ割り当てルーチン[ECP\_一覧](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体。 オペレーティング システムが ECP を自動的に解放されません\_リストの構造体。 代わりに、ECP 後\_リスト構造が割り当てられている、ミニフィルター ドライバーが最終的に呼び出す必要があります、 [ **FltFreeExtraCreateParameterList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist)または[ **FsRtlFreeExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff546005) ECP を解放するルーチン\_一覧。

2.  呼び出す、 [ **FltAllocateExtraCreateParameter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocateextracreateparameter)または[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)ページングされたメモリ割り当てルーチンプール ECP コンテキストの構造体と構造体へのポインターを生成します。

3.  呼び出す、 [ **FltInsertExtraCreateParameter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinsertextracreateparameter)または[ **FsRtlInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546179) ECP context 構造体を挿入するルーチン[ECP\_一覧](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体。

4.  呼び出す、 [ **IoInitializeDriverCreateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioinitializedrivercreatecontext)初期化ルーチンを[ **IO\_ドライバー\_作成\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_io_driver_create_context)構造体。

5.  定義、 [ **IO\_ドライバー\_作成\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_io_driver_create_context)構造体。 この定義では、ポイント、 **ExtraCreateParameter**のメンバー **IO\_ドライバー\_作成\_コンテキスト**を[ECP\_一覧](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体。

6.  呼び出す、 [ **FltCreateFileEx2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex2)または[ **IoCreateFileEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)に ECPs をアタッチするルーチン、 [ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)ファイルで操作します。 この呼び出しでへのポインターを渡す、 [ **IO\_ドライバー\_作成\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_io_driver_create_context)構造体を*DriverContext*パラメーター。

7.  呼び出す、 [ **FltFreeExtraCreateParameterList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist)または[ **FsRtlFreeExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff546005) を解放するルーチン[ECP\_一覧](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体。

 

 




