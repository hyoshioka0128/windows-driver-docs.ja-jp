---
title: UMDF でのフレームワーク要求オブジェクトの再利用
description: UMDF でのフレームワーク要求オブジェクトの再利用
ms.assetid: 804efc94-a7df-4ebd-a42e-82d1c5376e19
keywords:
- I/o 要求 WDK UMDF、オブジェクトの再利用
- 要求の処理 WDK UMDF、i/o 要求オブジェクトの再利用
- ユーザーモードドライバーフレームワーク WDK、i/o 要求オブジェクトの再利用
- UMDF WDK、i/o 要求オブジェクトの再利用
- ユーザーモードドライバー WDK UMDF、i/o 要求オブジェクトの再利用
- i/o 要求オブジェクトの再利用 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3130335a266cbec8578ad7beed9dd13e5b0ba86c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842226"
---
# <a name="reusing-framework-request-objects-in-umdf"></a>UMDF でのフレームワーク要求オブジェクトの再利用


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーのパフォーマンスを向上させるために、i/o ターゲットにほぼ同一の非同期要求を作成して送信するフレームワークベースのドライバーは、要求ごとに新しい要求オブジェクトを作成する代わりに、要求オブジェクトを再利用できます。 要求が完了すると、ドライバーは要求オブジェクトを再利用できます。

ドライバーが[**Iwdfdevice:: CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)を呼び出して要求オブジェクトを作成した場合、 [**IWDFIoRequest2:: 再利用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)を呼び出すことで要求を再利用できます。 また、ドライバーは、その i/o キュー内のフレームワークから受信した要求オブジェクトを再利用することもできます。

ドライバーが、再利用する要求オブジェクトに対して[**irequestcallback Requestcompletion:: OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)コールバック関数を提供している場合、ドライバーは[**再利用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)を呼び出した後で[**IWDFIoRequest:: setcompletion callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)を呼び出す必要があります。

 

 





