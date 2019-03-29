---
title: ミニフィルター ドライバーのインスタンスのスタックを渡すことの I/O 操作
description: 下のミニフィルター ドライバー インスタンス スタックへ I/O 操作を渡す
ms.assetid: b2661e1e-2190-4def-be6c-27057c631304
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、ドライバーのインスタンスのスタックを渡して
- ミニフィルター ドライバー スタック WDK ファイル システムを I/O ops を渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48079622557ad60edc9f96ab8390779024c194cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581983"
---
# <a name="passing-io-operations-down-the-minifilter-driver-instance-stack"></a>ミニフィルター ドライバーのインスタンスのスタックを渡すことの I/O 操作


## <span id="ddk_passing_an_io_operation_down_the_minifilter_instance_stack_if"></span><span id="DDK_PASSING_AN_IO_OPERATION_DOWN_THE_MINIFILTER_INSTANCE_STACK_IF"></span>


ミニフィルター ドライバーのときに[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)または作業ルーチンは、フィルター マネージャーに、I/O 操作を返します、フィルター マネージャーがミニフィルター ドライバーが次に、操作を送信します現在ミニフィルター ドライバーとレガシ フィルターをさらに処理するため、ファイル システム ミニフィルター ドライバーのインスタンスのスタックにします。

ミニフィルター ドライバーの preoperation コールバック ルーチンは、状態値は次のいずれかを返すことによってさらに処理フィルター マネージャーへの I/O 操作を返します。

-   FLT\_PREOP\_成功\_いいえ\_コールバック (すべての操作の種類)

-   FLT\_PREOP\_成功\_WITH\_コールバック (すべての操作の種類)

-   FLT\_PREOP\_同期 (IRP ベースの I/O 操作の場合のみ)

**注**  が FLT\_PREOP\_同期が返されますのみ IRP ベースの I/O 操作では、その他の操作の種類の場合は、この状態値を返すことができます。 フィルター マネージャーでは、FLT の場合と同様に、この戻り値が扱われます、IRP ベースの I/O 操作ではありませんが、I/O 操作の返された場合に\_PREOP\_成功\_WITH\_コールバック。

 

または、preoperation コールバック ルーチンで保留された操作の処理ルーチンを返します、I/O 操作フィルター マネージャーにで前の状態値のいずれかを渡すことによって、 *CallbackStatus*パラメーターと、呼び出し[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913) I/O の保留操作の処理を再開します。

このセクションの内容:

[返す FLT\_PREOP\_成功\_WITH\_コールバック](returning-flt-preop-success-with-callback.md)

[返す FLT\_PREOP\_成功\_いいえ\_コールバック](returning-flt-preop-success-no-callback.md)

[返す FLT\_PREOP\_同期](returning-flt-preop-synchronize.md)

 

 




