---
title: MSI 割り込みの登録と登録解除
description: MSI 割り込みの登録と登録解除
ms.assetid: 61bdcf8c-b56e-4ef9-b9db-407591ff2f95
keywords:
- MSI-X WDK ネットワーク, 割り込みの登録
- メッセージシグナルによる WDK ネットワークの割り込み、割り込みの登録
- Msi WDK ネットワーク, 割り込みの登録
- WDK ネットワークの割り込み、登録
- MSI-X WDK ネットワーク, 登録解除割り込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52f9b95ccebec27f59f1fae48541312fbd7d7f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842090"
---
# <a name="registering-and-deregistering-an-msi-interrupt"></a>MSI 割り込みの登録と登録解除





MSI サポートに登録するために、ミニポートドライバーは[**NdisMRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)関数を呼び出して msi 割り込みを登録します。 このドライバーは、割り込み特性と関数のエントリポイントを指定するために、 [**NDIS\_ミニポート\_割り込み\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics)の構造を割り当て、初期化します。 ドライバーは、NDIS\_ミニポート\_割り込み\_特性の構造の**msisupported**メンバーを**TRUE**に設定する必要があります。 次に、ドライバーは構造体を**NdisMRegisterInterruptEx**に渡します。

MSI 割り込みをサポートするには、次の関数を定義する必要があります。

-   [*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)

-   [*MiniportMessageInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc)

-   [*MiniportDisableMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_disable_message_interrupt)

-   [*MiniportEnableMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_enable_message_interrupt)

ミニポートドライバーは、ドライバーが MSI エントリポイントをサポートしている場合でも、次の一覧に示すように、行ベースの割り込み関数のエントリポイントを提供する必要があります。 NDIS が MSI 割り込みを許可しない場合は、フォールバック条件として通常の割り込みを許可できます。

行割り込み関数には、次のものがあります。

-   [*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)

-   [*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)

-   [*MiniportDisableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_disable_interrupt)

-   [*MiniportEnableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_enable_interrupt)

ドライバーは、以前に**NdisMRegisterInterruptEx**で割り当てられたリソースを解放するために、 [**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)関数を呼び出す必要があります。

 

 





