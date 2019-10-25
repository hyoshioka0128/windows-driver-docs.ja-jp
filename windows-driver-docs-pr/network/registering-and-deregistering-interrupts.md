---
title: 割り込みの登録と登録解除
description: 割り込みの登録と登録解除
ms.assetid: 222782f3-092e-417d-ab1b-1988a593caa4
keywords:
- WDK ネットワークの割り込み、登録
- WDK ネットワークの割り込み、登録解除
- NdisMRegisterInterruptEx
- NdisMDeregisterInterruptEx
- 登録 (割り込みを)
- 割り込みの登録解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3daf7e68925bfc5ade7efb6fcf4033736830ef1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842086"
---
# <a name="registering-and-deregistering-interrupts"></a>割り込みの登録と登録解除





ミニポートドライバーは、 [**NdisMRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)を呼び出して割り込みを登録します。 このドライバーは、割り込み特性と関数のエントリポイントを指定するために、 [**NDIS\_ミニポート\_割り込み\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics)の構造を割り当て、初期化します。 このドライバーは、構造体を**NdisMRegisterInterruptEx**に渡します。

ドライバーは、以前に**NdisMRegisterInterruptEx**で割り当てられたリソースを解放するために、 [**NdisMDeRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)関数を呼び出します。

 

 





