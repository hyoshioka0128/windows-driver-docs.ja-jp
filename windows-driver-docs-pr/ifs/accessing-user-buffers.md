---
title: ユーザー バッファーへのアクセス
description: ユーザー バッファーへのアクセス
ms.assetid: 5ab32074-0949-4cdc-8a95-1bded0085ce1
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、ユーザー バッファー
- バッファー WDK ファイル システム ミニフィルター
- ユーザー バッファー WDK ファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2421faf736146662add2de160fb1ac3ec61dbc33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379020"
---
# <a name="accessing-user-buffers"></a>ユーザー バッファーへのアクセス


バッファー記述子の一覧 (MDLs) メモリなど、特定の I/O 操作に固有のすべてのパラメーターが定義されている、 [ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)共用体。 共用体が含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)経由でアクセスする構造体、 **Iopb**メンバー[ **FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data) I/O 操作を表す構造体です。 フィルター マネージャーとミニフィルター ドライバーを使用して**FLT\_コールバック\_データ**を開始して、I/O 操作を処理する構造体。

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)共用体には、その操作に使用されるバッファリング メソッドに固有の IRP ベースの操作のパラメーターの定義も含まれています (バッファー、ダイレクト I/O、またはバッファーもダイレクト I/O)。 IRP ベース以外の操作 (高速な I/O および FsFilter コールバック ルーチン) のパラメーターの定義も含まれています。

ミニフィルター ドライバーが呼び出せる[ **FltDecodeParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdecodeparameters) MDL アドレスへのポインターを取得するポインター、バッファー長、および I/O 操作の必要なアクセス パラメーターのバッファーします。 これにより、複数の I/O 操作でこれらのパラメーターにアクセスするヘルパー ルーチンでこれらのパラメーターの位置を検索する switch ステートメントがなくなりますミニフィルター ドライバーが保存されます。

ユーザー バッファーに関連する I/O 操作を処理する際は、1 つが使用可能な場合、ミニフィルター ドライバーは常に、MDL を使用する必要があります。 ミニフィルター ドライバーを呼び出す必要がありますので場合、 [ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) MDL のシステムのアドレスを取得し、システム アドレス ユーザー バッファーへのアクセスを使用します。

バッファーのアドレスにしか使用できない場合ミニフィルター ドライバーは常に try/ブロックを除く、バッファーにアクセスする試みを囲む必要があります。 ミニフィルター ドライバーが同期されていない postoperation コールバック ルーチン内のバッファーにアクセスする必要がありますか、サイト サーバー場合は、I/O 操作がワーカー スレッドに投稿された、ミニフィルター ドライバーする必要がありますを呼び出してユーザー バッファーをロックします場合[  **。FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)します。 この関数は I/O 操作の種類に基づいて、ロックされているバッファーに適用する適切なアクセス方法を決定し、ロックされたページを指す MDL を作成します。

### <a name="span-idfiltermanagerroutinesforaccessinguserbuffersspanspan-idfiltermanagerroutinesforaccessinguserbuffersspanspan-idfiltermanagerroutinesforaccessinguserbuffersspanfilter-manager-routines-for-accessing-user-buffers"></a><span id="Filter_Manager_Routines_for_Accessing_User_Buffers"></span><span id="filter_manager_routines_for_accessing_user_buffers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_ACCESSING_USER_BUFFERS"></span>ユーザー バッファーにアクセスするためにマネージャーのルーチンをフィルター処理します。

フィルター マネージャーは、preoperation と postoperation コールバック ルーチン内のユーザーのバッファーにアクセスするため、次のサポート ルーチンを提供します。

[**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdecodeparameters)

[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)

 

 




