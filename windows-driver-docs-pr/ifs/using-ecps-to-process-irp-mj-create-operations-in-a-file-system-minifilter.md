---
title: ECPs を使用したファイルシステムフィルタードライバーの IRP_MJ_CREATE の処理
description: ファイル システム フィルター ドライバーで ECP を使用して IRP_MJ_CREATE 操作を処理する
ms.assetid: 969709a9-cdca-4a1a-95a0-0bb89cd17693
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: e579dd6851f295c50fd72705a01fcc8a654403c7
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74135154"
---
# <a name="using-ecps-to-process-irp_mj_create-operations-in-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーで ECP を使用して IRP_MJ_CREATE 操作を処理する

ファイルシステムフィルタードライバーで ECPs を使用すると、 [**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作を処理できます。 ファイルシステムフィルタードライバーは、次のセクションのルーチンを呼び出して、 **IRP_MJ_CREATE**操作の ecps の取得、確認、追加、および削除を行うことができます。 また、ECPs の発生元となるオペレーティングシステムの領域を決定することもできます。

## <a name="retrieving-ecps"></a>ECPs の取得

ファイルシステムフィルタードライバーは、次の手順に従って、 [**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作の ecps を取得できます。

1. [**FltGetEcpListFromCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetecplistfromcallbackdata)または[**FsRtlGetEcpListFromIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546015)ルーチンを呼び出して、作成操作に関連付けられている ECP コンテキスト構造リスト (ECP_LIST) へのポインターを取得します。

2. 次のいずれかの操作を実行します。
    - [**FltGetNextExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetnextextracreateparameter)または[**FsRtlGetNextExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546028)ルーチンを呼び出して、ecp リスト内の次の (または最初の) ecp コンテキスト構造へのポインターを取得します。
    - [**Fltfindextracreateparameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfindextracreateparameter)または[**fsrtlfindextracreateparameter**](https://msdn.microsoft.com/library/windows/hardware/ff545968)ルーチンを呼び出して、指定された種類の ECP コンテキスト構造を ecp リストで検索します。 構造が見つかった場合、どちらのルーチンも、ECP コンテキスト構造へのポインターを返します。

## <a name="setting-ecps"></a>ECPs の設定

[**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作に ecps を設定するには、まず、作成操作に関連付けられている既存の ECP コンテキスト構造リスト (ECP_LIST) をファイルシステムフィルタードライバーで取得するか、ECP_LIST と ecp コンテキスト構造を割り当てて、ECP_LIST に ecp コンテキスト構造を挿入します。

### <a name="setting-ecps-in-an-existing-ecp_list"></a>既存の ECP_LIST での ECPs の設定

ファイルシステムフィルタードライバーは、次の手順に従って、create 操作に関連付けられている既存の ECP_LIST に ECPs を設定できます。

1. [**FltGetEcpListFromCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetecplistfromcallbackdata)または[**FsRtlGetEcpListFromIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546015)ルーチンを呼び出して、作成操作に関連付けられている ECP コンテキスト構造リスト (ECP_LIST) へのポインターを取得します。

2. [**FltAllocateExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter)または[**FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)ルーチンを呼び出して、ECP コンテキスト構造にページングされたメモリプールを割り当て、その構造体へのポインターを生成します。

3. [**FltInsertExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter)または[**FsRtlInsertExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546179)ルーチンを呼び出して、 [ECP_LIST](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体に ECP コンテキスト構造を挿入します。

### <a name="setting-ecps-in-a-newly-created-ecp_list"></a>新しく作成された ECP_LIST での ECPs の設定

ファイルシステムフィルタードライバーは、次の手順に従って、作成操作に関連付けられている新しく作成された ECP_LIST に ECPs を設定できます。

1. [**FltAllocateExtraCreateParameterList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterlist)または[**FsRtlAllocateExtraCreateParameterList**](https://msdn.microsoft.com/library/windows/hardware/ff545632)ルーチンを呼び出して、 [ECP_LIST](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体にメモリを割り当てます。

2. [**FltAllocateExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter)または[**FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)ルーチンを呼び出して、ECP コンテキスト構造にページングされたメモリプールを割り当て、その構造体へのポインターを生成します。

3. [**FltInsertExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter)または[**FsRtlInsertExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546179)ルーチンを呼び出して、 [ECP_LIST](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))構造体に ECP コンテキスト構造を挿入します。

4. [**FltSetEcpListIntoCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetecplistintocallbackdata)または[**FsRtlSetEcpListIntoIrp**](https://msdn.microsoft.com/library/windows/hardware/ff547250)ルーチンを呼び出して、ECP リストを作成操作にアタッチします。

## <a name="removing-ecps"></a>ECPs の削除

ファイルシステムフィルタードライバーは、次の手順に従って、 [**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作の ecps を削除できます。

1. [**FltRemoveExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltremoveextracreateparameter)または[**FsRtlRemoveExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff547203)ルーチンを呼び出して、ECP の一覧で ecp コンテキスト構造を検索します。 ECP コンテキスト構造が見つかった場合、このルーチンは ecp のコンテキスト構造を ECP リストから切り離します。

2. デタッチされた ECP コンテキスト構造のメモリを解放するには、 [**FltFreeExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameter)または[**FsRtlFreeExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545989)ルーチンを呼び出します。 次のいずれかの方法でメモリを割り当てた場合は、これらのルーチンを呼び出して、ECP コンテキスト構造のメモリを解放できます。

    - [**FltAllocateExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter)または[**FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)ルーチンを呼び出して、ページングされたメモリプールを割り当てる
    - [**FltAllocateExtraCreateParameterFromLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterfromlookasidelist)または[**FsRtlAllocateExtraCreateParameterFromLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545616)ルーチンを呼び出して、ルックアサイドリストからメモリプールを割り当てました

## <a name="marking-ecps-as-acknowledged-or-determining-acknowledge-status"></a>ECPs を受信確認済みとしてマークするか、確認の状態を判断する

ファイルシステムフィルタードライバーは、次のルーチンを呼び出して、ECPs を確認済みとしてマークするか、ECPs が受信確認済みとしてマークされているかどうかを判断できます。

- [**FltAcknowledgeEcp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltacknowledgeecp)または[**FsRtlAcknowledgeEcp**](https://msdn.microsoft.com/library/windows/hardware/ff545574)ルーチンを呼び出して、ECP コンテキスト構造を確認済みとしてマークします。 ECP は、[確認済み]、[使用済み]、[処理済み]、または [その他の ECP] の任意の状態としてマークできます。

- [**FltIsEcpAcknowledged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisecpacknowledged)または[**FsRtlIsEcpAcknowledged**](https://msdn.microsoft.com/library/windows/hardware/ff546808)ルーチンを呼び出して、ECP コンテキスト構造が確認済みとしてマークされているかどうかを判断します。

## <a name="determining-origination-mode"></a>発信元モードの決定

ファイルシステムフィルタードライバーは、 [**Fltisecpfromusermode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisecpfromusermode)モードルーチンまたは[**Fsrtlisecpfromusermode**](https://msdn.microsoft.com/library/windows/hardware/ff546813)モードルーチンを呼び出して、ECP コンテキスト構造がユーザーモードからのものであるかどうかを判断できます。 ファイルシステムフィルタードライバーは、ユーザーモードからの ECP コンテキスト構造の受け入れを拒否することができます。

## <a name="using-lookaside-lists-to-allocate-ecps"></a>ルックアサイドリストを使用した ECPs の割り当て

ファイルシステムフィルタードライバーは、次のルーチンを呼び出して、ルック Ps をルックアサイドリストから割り当てたり、ルックアサイドリストと ECPs を管理したりすることができます。

- [**FltInitExtraCreateParameterLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitextracreateparameterlookasidelist)または[**FsRtlInitExtraCreateParameterLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff546102)ルーチンを呼び出して、固定の1つまたは複数の ECP コンテキスト構造の割り当てに使用される、ページングまたは非ページプールのルックアサイドリストを初期化します。幅.

- [**FltDeleteExtraCreateParameterLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeleteextracreateparameterlookasidelist)または[**FsRtlDeleteExtraCreateParameterLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545849)ルーチンを呼び出して、ルックアサイドリストを解放します。

- [**FltAllocateExtraCreateParameterFromLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterfromlookasidelist)または[**FsRtlAllocateExtraCreateParameterFromLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545616)ルーチンを呼び出して、ECP コンテキスト構造のルックアサイドリストからメモリプールを割り当て、それに対するポインターを生成します。データ.

- [**FltFreeExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameter)または[**FsRtlFreeExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545989)ルーチンを呼び出して、ECP コンテキスト構造のメモリを解放します。
