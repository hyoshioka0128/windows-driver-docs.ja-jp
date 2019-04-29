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
ms.openlocfilehash: 39c402f6273020944a585216bd8d77fb8d2129e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323129"
---
# <a name="accessing-user-buffers"></a>ユーザー バッファーへのアクセス


バッファー記述子の一覧 (MDLs) メモリなど、特定の I/O 操作に固有のすべてのパラメーターが定義されている、 [ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)共用体。 共用体が含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)経由でアクセスする構造体、 **Iopb**メンバー[ **FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620) I/O 操作を表す構造体です。 フィルター マネージャーとミニフィルター ドライバーを使用して**FLT\_コールバック\_データ**を開始して、I/O 操作を処理する構造体。

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)共用体には、その操作に使用されるバッファリング メソッドに固有の IRP ベースの操作のパラメーターの定義も含まれています (バッファー、ダイレクト I/O、またはバッファーもダイレクト I/O)。 IRP ベース以外の操作 (高速な I/O および FsFilter コールバック ルーチン) のパラメーターの定義も含まれています。

ミニフィルター ドライバーが呼び出せる[ **FltDecodeParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff541956) MDL アドレスへのポインターを取得するポインター、バッファー長、および I/O 操作の必要なアクセス パラメーターのバッファーします。 これにより、複数の I/O 操作でこれらのパラメーターにアクセスするヘルパー ルーチンでこれらのパラメーターの位置を検索する switch ステートメントがなくなりますミニフィルター ドライバーが保存されます。

ユーザー バッファーに関連する I/O 操作を処理する際は、1 つが使用可能な場合、ミニフィルター ドライバーは常に、MDL を使用する必要があります。 ミニフィルター ドライバーを呼び出す必要がありますので場合、 [ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) MDL のシステムのアドレスを取得し、システム アドレス ユーザー バッファーへのアクセスを使用します。

バッファーのアドレスにしか使用できない場合ミニフィルター ドライバーは常に try/ブロックを除く、バッファーにアクセスする試みを囲む必要があります。 ミニフィルター ドライバーが同期されていない postoperation コールバック ルーチン内のバッファーにアクセスする必要がありますか、サイト サーバー場合は、I/O 操作がワーカー スレッドに投稿された、ミニフィルター ドライバーする必要がありますを呼び出してユーザー バッファーをロックします場合[  **。FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)します。 この関数は I/O 操作の種類に基づいて、ロックされているバッファーに適用する適切なアクセス方法を決定し、ロックされたページを指す MDL を作成します。

### <a name="span-idfiltermanagerroutinesforaccessinguserbuffersspanspan-idfiltermanagerroutinesforaccessinguserbuffersspanspan-idfiltermanagerroutinesforaccessinguserbuffersspanfilter-manager-routines-for-accessing-user-buffers"></a><span id="Filter_Manager_Routines_for_Accessing_User_Buffers"></span><span id="filter_manager_routines_for_accessing_user_buffers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_ACCESSING_USER_BUFFERS"></span>ユーザー バッファーにアクセスするためにマネージャーのルーチンをフィルター処理します。

フィルター マネージャーは、preoperation と postoperation コールバック ルーチン内のユーザーのバッファーにアクセスするため、次のサポート ルーチンを提供します。

[**FltDecodeParameters**](https://msdn.microsoft.com/library/windows/hardware/ff541956)

[**FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)

 

 




