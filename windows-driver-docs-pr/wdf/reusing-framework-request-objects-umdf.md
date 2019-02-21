---
title: UMDF で Framework 要求オブジェクトを再利用
description: UMDF で Framework 要求オブジェクトを再利用
ms.assetid: 804efc94-a7df-4ebd-a42e-82d1c5376e19
keywords:
- I/O 要求の WDK UMDF、オブジェクトを再利用
- 要求の処理の WDK UMDF、I/O 要求オブジェクトを再利用
- ユーザー モード ドライバー フレームワーク WDK は、I/O 要求オブジェクトを再利用
- UMDF WDK、I/O 要求オブジェクトを再利用
- 要求オブジェクトをユーザー モード ドライバー WDK UMDF、I/O を再利用
- WDK UMDF オブジェクトを再利用の I/O 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19ffa2641991b83a35abade8ec15b182f206500e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556919"
---
# <a name="reusing-framework-request-objects-in-umdf"></a>UMDF で Framework 要求オブジェクトを再利用


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーのパフォーマンスを向上させるのには、framework ベースのドライバーを作成し、送信多くほぼ I/O のターゲットに同一の非同期要求を再利用できるは、要求ごとに新しい要求オブジェクトを作成する代わりにオブジェクトを要求します。 ドライバーは、要求が完了した後、要求オブジェクトを再利用できます。

ドライバーが呼び出すことによって、要求オブジェクトを作成してかどうか[ **IWDFDevice::CreateRequest**](https://msdn.microsoft.com/library/windows/hardware/ff557021)、呼び出すことによって、要求を再利用できます[ **IWDFIoRequest2::Reuse**](https://msdn.microsoft.com/library/windows/hardware/ff559048). ドライバーでは、その I/O キューのフレームワークから受信した要求オブジェクトを再利用もできます。

お使いのドライバーの場合、 [ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)ドライバーに呼び出す必要がありますが再利用する要求オブジェクトのコールバック関数、 [ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)呼び出した後[**再利用**](https://msdn.microsoft.com/library/windows/hardware/ff559048)します。

 

 





