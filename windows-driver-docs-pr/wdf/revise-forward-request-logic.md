---
title: 転送要求のロジックを修正する
description: 転送要求のロジックを修正する
ms.assetid: B307AE04-7AA5-453D-9086-CD740617C659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74f0fe612b2adab674dd4356ea380f4e73b18013
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842202"
---
# <a name="revise-forward-request-logic"></a>転送要求のロジックを修正する


ドライバーが要求をそれ自体によって完了できない場合は、要求をスタックから次の下位のドライバーに渡します。 WDF ドライバーの場合、次に低いドライバーは既定の i/o ターゲットと見なされ、WDFIOTARGET オブジェクトによって表されます。 このオブジェクトへのハンドルを取得するために、ドライバーは[**Wdfdevicegetiotarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)を呼び出します。

WDF ドライバーがスタック内の次に低いドライバーに要求を渡す方法の詳細については、「 [I/o 要求の転送](forwarding-i-o-requests.md)」を参照してください。

 

 





