---
title: キャンセルされた要求のロジックを修正する
description: キャンセルされた要求のロジックを修正する
ms.assetid: 8246826A-BDBD-4A9B-9FFC-B813033E0FDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fc56a011372c388de87ca952d5d4b8b9bfd61c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325176"
---
# <a name="revise-canceled-request-logic"></a>キャンセルされた要求のロジックを修正する


I/O 要求が取り消されると、WDM ドライバーは、いくつかの困難な競合状態を管理する必要があります。 キューまたはドライバーが処理中には、要求をキャンセル可能性があります。 各ケースで、ドライバーをキャンセルし、要求の完了を 1 回だけであることを確認するのにロックの組み合わせを使用する必要があります。

WDF のキュー メカニズムには、キャンセルが大幅に簡略化します。 キューで実行されるときに、要求が取り消された場合、フレームワークは、ドライバーを通知することがなくキャンセルを処理します。 ドライバーは登録することで通知を要求することができます、 [ *EvtIoCanceledOnQueue* ](https://msdn.microsoft.com/library/windows/hardware/ff541756)コールバック関数。 フレームワークは、ドライバーに要求を配信するが、後に、要求は既定では取り消し可能ではありません。 ドライバーを呼び出すことができます[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)いつでも、要求がキャンセルされたかどうかを確認します。

詳細については、次を参照してください。 [I/O 要求のキャンセル](canceling-i-o-requests.md)します。

 

 





