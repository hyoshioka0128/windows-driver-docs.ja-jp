---
title: カーネル モード ドライバーで発生した irp_mj_create 用 Operations に ECPs をアタッチします。
description: カーネルモード ドライバーが開始した IRP_MJ_CREATE 操作に ECP をアタッチする
ms.assetid: 87daa861-b0d5-4877-bf16-fad120108de6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9dcefe4fd0ed16d9e5a29dab94d72ead78cf602
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393039"
---
# <a name="attaching-ecps-to-irpmjcreate-operations-that-a-kernel-mode-driver-originated"></a>IRP への ECPs\_MJ\_作成操作、カーネル モード ドライバーで発生しました。


次の手順を実行 ECPs を設定する ECPs をアタッチする必要があります、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)ファイルの操作。

1.  呼び出す、 [ **FltAllocateExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff541741)または[ **FsRtlAllocateExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff545632)メモリ割り当てルーチン[ECP\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff540148)構造体。 オペレーティング システムが ECP を自動的に解放されません\_リストの構造体。 代わりに、ECP 後\_リスト構造が割り当てられている、ミニフィルター ドライバーが最終的に呼び出す必要があります、 [ **FltFreeExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff542964)または[ **FsRtlFreeExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff546005) ECP を解放するルーチン\_一覧。

2.  呼び出す、 [ **FltAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff541728)または[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)ページングされたメモリ割り当てルーチンプール ECP コンテキストの構造体と構造体へのポインターを生成します。

3.  呼び出す、 [ **FltInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff543305)または[ **FsRtlInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546179) ECP context 構造体を挿入するルーチン[ECP\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff540148)構造体。

4.  呼び出す、 [ **IoInitializeDriverCreateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548419)初期化ルーチンを[ **IO\_ドライバー\_作成\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff548565)構造体。

5.  定義、 [ **IO\_ドライバー\_作成\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff548565)構造体。 この定義では、ポイント、 **ExtraCreateParameter**のメンバー **IO\_ドライバー\_作成\_コンテキスト**を[ECP\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff540148)構造体。

6.  呼び出す、 [ **FltCreateFileEx2** ](https://msdn.microsoft.com/library/windows/hardware/ff541939)または[ **IoCreateFileEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548283)に ECPs をアタッチするルーチン、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)ファイルで操作します。 この呼び出しでへのポインターを渡す、 [ **IO\_ドライバー\_作成\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff548565)構造体を*DriverContext*パラメーター。

7.  呼び出す、 [ **FltFreeExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff542964)または[ **FsRtlFreeExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff546005) を解放するルーチン[ECP\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff540148)構造体。

 

 




