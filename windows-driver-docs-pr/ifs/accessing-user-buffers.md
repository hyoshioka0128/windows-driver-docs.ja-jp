---
title: ユーザー バッファーへのアクセス
description: ユーザー バッファーへのアクセス
ms.assetid: 5ab32074-0949-4cdc-8a95-1bded0085ce1
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、ユーザーバッファー
- WDK ファイルシステムミニフィルターのバッファー
- ユーザーバッファー WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 653806bc1e091cc01d259b877ecf2990f8a482e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841500"
---
# <a name="accessing-user-buffers"></a>ユーザー バッファーへのアクセス


バッファーやメモリ記述子リスト (MDLs) など、特定の i/o 操作に固有のすべてのパラメーターは、 [**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)共用体で定義されています。 この共用体は、i/o 操作を表す[**FLT\_CALLBACK\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)構造体の**Iopb**メンバーを介してアクセスされる、 [**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。 フィルターマネージャーとミニフィルタードライバーはどちらも、 **FLT\_コールバック\_データ**構造を使用して、i/o 操作を開始および処理します。

また、 [**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)共用体には、その操作に使用されるバッファリングメソッド (バッファー、ダイレクト i/o、バッファーなしまたは直接 i/o) に固有の、IRP ベースの操作のパラメーター定義も含まれています。 また、非 IRP ベースの操作 (fast i/o および FsFilter コールバックルーチン) のパラメーター定義も含まれています。

ミニフィルタードライバーは、 [**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters)を呼び出して、i/o 操作の MDL アドレス、バッファーポインター、バッファー長、および必要なアクセスパラメーターへのポインターを取得できます。 これにより、これらのパラメーターを複数の i/o 操作にわたってアクセスするヘルパールーチンでこれらのパラメーターの位置を検索する switch ステートメントを使用して、ミニフィルタードライバーが保存されます。

ユーザーバッファーを含む i/o 操作を処理する場合、ミニフィルタードライバーは常に、使用可能な場合は MDL を使用する必要があります。 その場合、ミニフィルタードライバーは[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出して、MDL のシステムアドレスを取得し、システムアドレスを使用してユーザーバッファーにアクセスします。

バッファーアドレスだけが使用可能な場合、ミニフィルタードライバーは、try/except ブロック内のバッファーにアクセスする試行を常に囲む必要があります。 ミニフィルタードライバーが、同期されていない postoperation コールバックルーチン内のバッファーにアクセスする必要がある場合、または i/o 操作がワーカースレッドにポストされた場合は、 [**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)を呼び出すことによって、ミニフィルタードライバーでもユーザーバッファーをロックする必要があります。 この関数は、i/o 操作の種類に基づいて、ロックされたバッファーに適用する適切なアクセス方法を決定し、ロックされたページを指す MDL を作成します。

### <a name="span-idfilter_manager_routines_for_accessing_user_buffersspanspan-idfilter_manager_routines_for_accessing_user_buffersspanspan-idfilter_manager_routines_for_accessing_user_buffersspanfilter-manager-routines-for-accessing-user-buffers"></a><span id="Filter_Manager_Routines_for_Accessing_User_Buffers"></span><span id="filter_manager_routines_for_accessing_user_buffers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_ACCESSING_USER_BUFFERS"></span>ユーザーバッファーにアクセスするためのフィルターマネージャールーチン

フィルターマネージャーには、preoperation および postoperation コールバックルーチンでユーザーバッファーにアクセスするための次のサポートルーチンが用意されています。

[**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters)

[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)

 

 




