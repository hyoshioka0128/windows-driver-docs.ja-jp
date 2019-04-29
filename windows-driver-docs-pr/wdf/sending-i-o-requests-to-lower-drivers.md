---
title: 下位ドライバーへの I/O 要求の送信
description: 下位ドライバーへの I/O 要求の送信
ms.assetid: 89868b4d-e2c1-4f38-b81e-a96b8cff3e4f
keywords:
- I/O 要求の WDK UMDF、下位のドライバー
- 要求の WDK UMDF、下位のドライバーの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1d8471a29a645cd427643b603381f7aa1651482
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325148"
---
# <a name="sending-io-requests-to-lower-drivers"></a>下位ドライバーへの I/O 要求の送信


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーでは、完全に処理できない I/O 要求を受け取る、ドライバーは通常、スタックで [次へ] の下位のドライバーを受信した要求を転送します。 ドライバーの呼び出し、 [ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)メソッド要求を転送します。 同期的に転送するには、ドライバーは、WDF を渡します。\_要求\_送信\_オプション\_同期フラグ、*フラグ*パラメーター。 それ以外の場合、ドライバーは、要求を非同期的に転送します。 ドライバーは、要求を転送する前に完了ルーチンを登録する必要があります。 詳細については、次を参照してください。 [I/O 要求の完了](completing-i-o-requests.md)します。

 

 





