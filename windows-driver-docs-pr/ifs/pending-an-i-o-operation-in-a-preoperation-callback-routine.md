---
title: 操作前コールバック ルーチン内で I/O 操作を保留にする
description: 操作前コールバック ルーチン内で I/O 操作を保留にする
ms.assetid: 39b04911-c0d9-42ec-b93e-b440b12f9e41
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、保留中の操作
- 保留中のコールバック ルーチン WDK で I/O 操作は、ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c28659e301e7e85bc0db0319cec681159173430
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572947"
---
# <a name="pending-an-io-operation-in-a-preoperation-callback-routine"></a>操作前コールバック ルーチン内で I/O 操作を保留にする


## <span id="ddk_pending_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルター ドライバーの[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)システム ワーク キューに操作を投稿し、FLT を返すことで、I/O の保留操作をできる\_PREOP\_保留します。 ミニフィルター ドライバーも、それを呼び出すまでには、I/O 操作のコントロールを保持は、この状態値を返すことを示します[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913) I/O 操作の処理を再開します。

次の手順を実行することによってミニフィルター ドライバーの preoperation コールバック日常的なアプリケーション、I/O 操作:

1.  などのルーチンを呼び出すことによってシステムの作業キューに I/O 操作の転記[ **FltQueueDeferredIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff543449)します。

2.  返す FLT\_PREOP\_保留します。

ミニフィルター ドライバーを保留する必要がありますすべて (またはほとんど) の受信 I/O 操作はなどのルーチンを使用しない**FltQueueDeferredIoWorkItem**保留中の操作をこのルーチンを呼び出すと、システムが作業キューに送信するためです。 代わりに、このようなミニフィルター ドライバーには、キャンセルの安全なキューを使用する必要があります。 キャンセルの安全なキューの使用に関する詳細については、次を参照してください。 [ *FltCbdqInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff541802)します。

なおへの呼び出し**FltQueueDeferredIoWorkItem**次の条件のいずれかに該当する場合は失敗します。

-   操作は IRP ベースの I/O 操作ではありません。

-   ページング I/O 操作にします。

-   **TopLevelIrp** 、現在のスレッドのフィールドがない**NULL**します。 (このフィールドの値を検索する方法の詳細については、次を参照してください[ **IoGetTopLevelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548405)。)。

-   I/O 操作のターゲット インスタンスが破棄されています。

ミニフィルター ドライバーの preoperation 場合、コールバック ルーチンは FLT を返します\_PREOP\_保留中、返す必要があります**NULL**で、 *CompletionContext*出力パラメーター。

ミニフィルター ドライバーが FLT を返す\_PREOP\_PENDING IRP ベースの I/O 操作に対してのみです。 操作が IRP ベースの I/O 操作であるかどうかを確認するのには、使用、 [ **FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)マクロ。

I/O 操作を処理する作業ルーチンを呼び出す必要があります**FltCompletePendedPreOperation**操作の処理を再開します。

 

 




