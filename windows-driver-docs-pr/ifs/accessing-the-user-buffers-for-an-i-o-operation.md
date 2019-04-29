---
title: I/O 操作用のユーザー バッファーへのアクセス
description: I/O 操作用のユーザー バッファーへのアクセス
ms.assetid: 0f4334bf-eec9-4667-af02-537e3357d872
keywords:
- バッファー WDK ファイル システム ミニフィルター
- FLT_PARAMETERS
- メモリの記述子が WDK ファイル システム ミニフィルターを一覧表示します。
- MDLs WDK ファイル システム
- ファイル システムの I/O の WDK
- WDK の I/O 操作の IRP に基づくファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4be47d8817a10fea2477b0d51c37f9d8d80712d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323375"
---
# <a name="accessing-the-user-buffers-for-an-io-operation"></a>I/O 操作用のユーザー バッファーへのアクセス


## <span id="ddk_accessing_the_user_buffers_for_an_io_operation_if"></span><span id="DDK_ACCESSING_THE_USER_BUFFERS_FOR_AN_IO_OPERATION_IF"></span>


[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) I/O 操作には、バッファーのアドレスを含む、操作の操作に固有のパラメーターが含まれていますメモリ記述子の一覧を示します (MDL) の構造体。操作で使用されているすべてのバッファー。

IRP ベースの I/O 操作の場合を使用して、操作のバッファーを指定できます。

-   MDL のみ (通常は I/O のページング)

-   バッファーのアドレスのみ

-   バッファーのアドレスと MDL

高速な I/O 操作では、ユーザー空間バッファーのアドレスを指定します。 バッファーが高速の I/O 操作では、常にバッファーもダイレクト I/O を使用し、したがって MDL パラメーターを指定することはありません。

次のトピックがミニフィルター ドライバーの IRP ベースおよび高速の I/O 操作のバッファーのアドレスと MDLs を処理するためのガイドラインを提供[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)と[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107):

[Preoperation コールバック ルーチンでユーザー バッファーへのアクセス](accessing-user-buffers-in-a-preoperation-callback-routine.md)

[Postoperation コールバック ルーチンでユーザー バッファーへのアクセス](accessing-user-buffers-in-a-postoperation-callback-routine.md)

 

 




