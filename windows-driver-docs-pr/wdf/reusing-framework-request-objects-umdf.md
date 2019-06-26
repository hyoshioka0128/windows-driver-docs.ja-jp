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
ms.openlocfilehash: 2fc4816f100b724d8bf2b6561a9a6cf2569f4806
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376243"
---
# <a name="reusing-framework-request-objects-in-umdf"></a>UMDF で Framework 要求オブジェクトを再利用


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーのパフォーマンスを向上させるのには、framework ベースのドライバーを作成し、送信多くほぼ I/O のターゲットに同一の非同期要求を再利用できるは、要求ごとに新しい要求オブジェクトを作成する代わりにオブジェクトを要求します。 ドライバーは、要求が完了した後、要求オブジェクトを再利用できます。

ドライバーが呼び出すことによって、要求オブジェクトを作成してかどうか[ **IWDFDevice::CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createrequest)、呼び出すことによって、要求を再利用できます[ **IWDFIoRequest2::Reuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-reuse). ドライバーでは、その I/O キューのフレームワークから受信した要求オブジェクトを再利用もできます。

お使いのドライバーの場合、 [ **IRequestCallbackRequestCompletion::OnCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)ドライバーに呼び出す必要がありますが再利用する要求オブジェクトのコールバック関数、 [ **IWDFIoRequest::SetCompletionCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)呼び出した後[**再利用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)します。

 

 





