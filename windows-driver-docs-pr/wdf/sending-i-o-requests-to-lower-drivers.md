---
title: 下位ドライバーへの I/O 要求の送信
description: 下位ドライバーへの I/O 要求の送信
ms.assetid: 89868b4d-e2c1-4f38-b81e-a96b8cff3e4f
keywords:
- I/O 要求の WDK UMDF、下位のドライバー
- 要求の WDK UMDF、下位のドライバーの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc63ac09d5221da446fe7148ffaeb3a2daa51daf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376212"
---
# <a name="sending-io-requests-to-lower-drivers"></a>下位ドライバーへの I/O 要求の送信


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーでは、完全に処理できない I/O 要求を受け取る、ドライバーは通常、スタックで [次へ] の下位のドライバーを受信した要求を転送します。 ドライバーの呼び出し、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッド要求を転送します。 同期的に転送するには、ドライバーは、WDF を渡します。\_要求\_送信\_オプション\_同期フラグ、*フラグ*パラメーター。 それ以外の場合、ドライバーは、要求を非同期的に転送します。 ドライバーは、要求を転送する前に完了ルーチンを登録する必要があります。 詳細については、次を参照してください。 [I/O 要求の完了](completing-i-o-requests.md)します。

 

 





