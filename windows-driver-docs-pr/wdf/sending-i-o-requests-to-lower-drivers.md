---
title: 下位ドライバーへの I/O 要求の送信
description: 下位ドライバーへの I/O 要求の送信
ms.assetid: 89868b4d-e2c1-4f38-b81e-a96b8cff3e4f
keywords:
- I/o 要求 WDK UMDF、低ドライバー
- 要求の処理 WDK UMDF、低ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a8f50cc9663bac95b676a7da82f48b7f0ed4d71
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209946"
---
# <a name="sending-io-requests-to-lower-drivers"></a>下位ドライバーへの I/O 要求の送信


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーは、完全に処理できない i/o 要求を受信すると、通常、受信した要求をスタック内の次に小さいドライバーに転送します。 ドライバーは、 [**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出して要求を転送します。 同期的に転送するために、ドライバーは、 *Flags*パラメーターに\_オプション\_同期フラグを送信\_、WDF\_要求を渡します。 それ以外の場合、ドライバーは要求を非同期的に転送します。 ドライバーは、要求を転送する前に、完了ルーチンを登録する必要があります。 詳細については、「 [I/o 要求の完了](completing-i-o-requests.md)」を参照してください。

 

 





