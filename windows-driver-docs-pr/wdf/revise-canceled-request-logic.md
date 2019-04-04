---
title: 要求の取り消しロジックを修正します。
description: 要求の取り消しロジックを修正します。
ms.assetid: 8246826A-BDBD-4A9B-9FFC-B813033E0FDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fc56a011372c388de87ca952d5d4b8b9bfd61c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560936"
---
# <a name="revise-canceled-request-logic"></a>要求の取り消しロジックを修正します。


I/O 要求が取り消されると、WDM ドライバーは、いくつかの困難な競合状態を管理する必要があります。 キューまたはドライバーが処理中には、要求をキャンセル可能性があります。 各ケースで、ドライバーをキャンセルし、要求の完了を 1 回だけであることを確認するのにロックの組み合わせを使用する必要があります。

WDF のキュー メカニズムには、キャンセルが大幅に簡略化します。 キューで実行されるときに、要求が取り消された場合、フレームワークは、ドライバーを通知することがなくキャンセルを処理します。 ドライバーは登録することで通知を要求することができます、 [ *EvtIoCanceledOnQueue* ](https://msdn.microsoft.com/library/windows/hardware/ff541756)コールバック関数。 フレームワークは、ドライバーに要求を配信するが、後に、要求は既定では取り消し可能ではありません。 ドライバーを呼び出すことができます[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)いつでも、要求がキャンセルされたかどうかを確認します。

詳細については、[I/O 要求のキャンセル](canceling-i-o-requests.md)を参照してください。

 

 





