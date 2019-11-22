---
title: I/O 操作用のパラメーターの修正
description: I/O 操作用のパラメーターの修正
ms.assetid: 8e25842f-6f10-412f-8cb2-156bea7d7983
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、パラメーターの変更
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、パラメーターの変更
- ファイルシステムミニフィルタードライバー WDK、i/o パラメーターの変更
- ミニフィルタードライバー WDK、i/o パラメーターの変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 722c396c4169b887d11958e104c00fe3f903690c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841121"
---
# <a name="modifying-the-parameters-for-an-io-operation"></a>I/O 操作用のパラメーターの修正


## <span id="ddk_modifying_the_parameters_for_an_io_operation_if"></span><span id="DDK_MODIFYING_THE_PARAMETERS_FOR_AN_IO_OPERATION_IF"></span>


ミニフィルタードライバーは、i/o 操作のパラメーターを変更できます。 たとえば、ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)は、操作のターゲットインスタンスを変更することで、i/o 操作を別のボリュームにリダイレクトできます。 新しいターゲットインスタンスは、別のボリュームの同じ高度な同じミニフィルタードライバーのインスタンスである必要があります。

I/o 操作のパラメーターは、操作のコールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体と i/o パラメーターブロック ([**FLT\_IO\_parameter\_block**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)) 構造体にあります。 ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)と[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)は、*データ*入力パラメーター内の操作のコールバックデータ構造へのポインターを受け取ります。 コールバックデータ構造体の*Iopb*メンバーは、操作のパラメーターを含む i/o パラメーターブロック構造体へのポインターです。

ミニフィルタードライバーの preoperation コールバックルーチンによって i/o 操作のパラメーターが変更された場合、ミニフィルタードライバーインスタンススタック内のミニフィルタードライバーの下にあるすべてのミニフィルタードライバーは、変更されたパラメーターを preoperation に受け取り、postoperation コールバックルーチン。

修正されたパラメーターは、現在のミニフィルタードライバーの postoperation コールバックルーチン、またはミニフィルタードライバーインスタンススタック内のミニフィルタードライバーであるミニフィルタードライバーによって受け取られません。 どのような状況でも、ミニフィルタードライバーの preoperation および postoperation コールバックルーチンは、指定された i/o 操作に対して同じ入力パラメーター値を受け取ります。

I/o 操作のパラメーターを変更した後、preoperation または postoperation コールバックルーチンは、コールバックデータ構造の**Iostatus**フィールドの内容が変更されていない限り、 [**FltSetCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)を呼び出すことによってこれを実行したことを示す必要があります。 それ以外の場合、フィルターマネージャーは、パラメーター値に対する変更をすべて無視します。 **FltSetCallbackDataDirty**は、i/o 操作のコールバックデータ構造で FLTFL\_CALLBACK\_DATA\_DIRTY フラグを設定します。 ミニフィルタードライバーでは、 [**Fltiscallbackdatadirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltiscallbackdatadirty)を呼び出すか、 [**Fltclearbackdatadirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclearcallbackdatadirty)を呼び出してクリアすることで、このフラグをテストできます。

ミニフィルタードライバーの preoperation コールバックルーチンによって i/o 操作のパラメーターが変更された場合、ミニフィルタードライバーインスタンススタック内のミニフィルタードライバーの下にあるすべてのミニフィルタードライバーは、*データ* *内の変更されたパラメーターを受け取ります。FltObjects*および postoperation コールバックルーチンに入力パラメーターを入力します。 (ミニフィルタードライバーは、 *FltObjects*パラメーターによってポイントされる[**FLT\_関連\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_related_objects)構造の内容を直接変更することはできません。 ただし、ミニフィルタードライバーによって、i/o 操作の対象インスタンスまたはターゲットファイルオブジェクトが変更された場合は、フィルターマネージャーによって、対応する**インスタンス**の値または FLT\_関連する\_オブジェクトの**FileObject**メンバーの値が変更されます。より低いミニフィルタードライバーに渡される構造体。)

ミニフィルタードライバーの preoperation コールバックルーチンによって実行されるパラメーター変更は、ミニフィルタードライバーの独自の postoperation コールバックルーチンによって受信されませんが、preoperation コールバックルーチンは、変更されたパラメーターに関する情報を渡すことができます。ミニフィルタードライバーの独自の postoperation コールバックルーチン。 Preoperation コールバックルーチンが、FLT\_PREOPERATION\_SUCCESS\_を返すことによってスタックに i/o 操作を渡した場合、\_CALLBACK または FLT\_PREOPERATION\_SYNCHRONIZE では、変更されたパラメーターに関する情報を格納できます。値は、完了後*の出力パラメーター*によってポイントされる、ミニフィルタで定義された構造になります。 フィルターマネージャー*は、完了後の入力パラメーター*にこの構造体のポインターを postoperation コールバックルーチンに渡します。

I/o 操作のパラメーターの詳細については、「 [**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) 」および「 [**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)」を参照してください。

 

 




