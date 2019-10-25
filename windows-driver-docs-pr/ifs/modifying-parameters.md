---
title: パラメーターの修正
description: パラメーターの修正
ms.assetid: 01accd7f-7aa6-4f83-b8b4-81c04cd48dac
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、パラメーターの変更
- スワップバッファー WDK ファイルシステムミニフィルター
- WDK ファイルシステムミニフィルターのバッファー
- メモリ記述子に WDK ファイルシステムミニフィルターが一覧表示されます。
- MDLs WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 785bfedce288f30319ebbae697a252c77e7cbd80
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841122"
---
# <a name="modifying-parameters"></a>パラメーターの修正


ミニフィルタードライバーでは、ターゲットインスタンス、ターゲットファイルオブジェクト、バッファーアドレスやメモリ記述子リスト (MDL) アドレスなどの操作固有のパラメーターなど、i/o 操作に関連付けられている特定のパラメーターを変更できます。 ミニフィルタードライバーは、通常、i/o 要求に対して事前操作コールバックのパラメーターを変更します。 ミニフィルタードライバーでパラメーターが変更された場合、パラメーターが変更されたことをフィルターマネージャーに通知するには、 [**FltSetCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)を呼び出す必要があります。 また、preoperation コールバックから渡されたコンテキストの変更を記録して、ポスト操作コールバックで使用できるようにする必要があります。

ミニフィルタードライバーは、preoperation コールバックで操作を完了したとき、または postoperation コールバックで操作が失敗したときに、操作の i/o 状態を変更することができます (状態\_成功をエラー状態に変更するなど)。 この場合、 [**FltSetCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)を呼び出す必要はありません。

パラメーターの変更の詳細については、「 [I/o 操作のパラメーターの変更](modifying-the-parameters-for-an-i-o-operation.md)」を参照してください。

ミニフィルタードライバーは、i/o 要求のバッファーフィールドを独自のバッファーに置き換えることによって、バッファーのスワップを行うことができます。 このようなミニフィルタードライバーは、i/o 要求の MDL およびバッファーフィールドの同期を維持する役割を担います。フィルターマネージャーは、バッファーがシステムバッファーであるかどうかを示すために、 [**FLT\_callback\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)構造で、FLTFL\_CALLBACK\_DATA\_SYSTEM\_BUFFER\_フラグを設定します。その場合、ミニフィルタードライバーは、非ページプールから交換バッファーを割り当て、MDL フィールドを**NULL**に設定する必要があります。 それ以外の場合は、ページングされたプールまたは非ページプールからバッファーを割り当てることができ、ミニフィルタードライバーでは常に MDL を作成して設定する必要があります。 (高速な i/o 操作の場合は、ページングされたプールまたは非ページプールから新しいバッファーを割り当て、MDL を**NULL**にする必要があります)。ミニフィルタードライバーは、置き換えられるバッファーまたは MDL を解放しないようにする必要があります。また、コールバックデータ構造に正常に挿入された MDL を解放することはできません (フィルターマネージャーによって、ミニフィルタードライバーの代わりに MDL が解放されます)。 MDL またはバッファーに変更を加えた後、ミニフィルタードライバーは[**FltSetCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)を呼び出す必要があります。

ミニフィルタードライバーは、バッファーを交換するすべての操作に対して postoperation コールバックを登録する必要があります。 このコールバックルーチンでは、ミニフィルタードライバーは、割り当てられたバッファーを解放する必要があります。 フィルターマネージャーは、ミニフィルタードライバーが[**FltRetainSwappedBufferMdlAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltretainswappedbuffermdladdress)を呼び出す場合を除き、MDL を解放します。この場合、ミニフィルタードライバーによって、MDL が解放されます。 ミニフィルタードライバーは、 [**FltGetSwappedBufferMdlAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetswappedbuffermdladdress)を呼び出して、preoperation コールバックでバッファーセットの MDL を取得できます。

バッファーをスワップした操作中にミニフィルタードライバーがアンロードされた場合、操作を "ドレイン" することはできません。代わりに、操作は取り消され、フィルタマネージャーは、ミニフィルタードライバーをアンロードする前に操作が完了するのを待機します。

バッファーを交換するミニフィルタードライバーの例については、SwapBuffers サンプルを参照してください。

### <a name="span-idfilter_manager_routines_for_modifying_parametersspanspan-idfilter_manager_routines_for_modifying_parametersspanspan-idfilter_manager_routines_for_modifying_parametersspanfilter-manager-routines-for-modifying-parameters"></a><span id="Filter_Manager_Routines_for_Modifying_Parameters"></span><span id="filter_manager_routines_for_modifying_parameters"></span><span id="FILTER_MANAGER_ROUTINES_FOR_MODIFYING_PARAMETERS"></span>パラメーターを変更するためのフィルターマネージャールーチン

フィルターマネージャーには、preoperation および postoperation コールバックルーチンで i/o 操作パラメーターを変更するための次のサポートルーチンが用意されています。

[**Fltclearの Datadirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclearcallbackdatadirty)

[**FltIsCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltiscallbackdatadirty)

[**FltSetCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)

次のルーチンでは、バッファーのスワップがサポートされています。

[**FltGetSwappedBufferMdlAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetswappedbuffermdladdress)

[**FltRetainSwappedBufferMdlAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltretainswappedbuffermdladdress)

 

 




