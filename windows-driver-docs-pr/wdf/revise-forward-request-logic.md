---
title: 転送要求のロジックを修正する
description: 転送要求のロジックを修正する
ms.assetid: B307AE04-7AA5-453D-9086-CD740617C659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed6d1d8123a061ea9f4237fdf2d3de66285de193
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376232"
---
# <a name="revise-forward-request-logic"></a>転送要求のロジックを修正する


ドライバーは、単独で要求を完了することはできません、[次へ] の下のドライバーに下位のスタックの要求が渡されます。 WDF のドライバーの場合、[次へ] の下のドライバーと見なされ、既定の I/O ターゲット WDFIOTARGET オブジェクトによって表されます。 ドライバーの呼び出しは、このオブジェクトを識別するハンドルを取得する[ **WdfDeviceGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)します。

WDF のドライバーがスタックで、[次へ] の下のドライバーに要求を渡す方法については、次を参照してください。 [I/O 要求の転送](forwarding-i-o-requests.md)します。

 

 





