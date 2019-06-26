---
title: MSI 割り込みの登録および登録解除
description: MSI 割り込みの登録および登録解除
ms.assetid: 61bdcf8c-b56e-4ef9-b9db-407591ff2f95
keywords:
- MSI X WDK ネットワーク、割り込みを登録します。
- メッセージ シグナル割り込み WDK ネットワー キング、割り込みを登録します。
- Msi WDK ネットワー キング、割り込みを登録します。
- ネットワーク、登録に WDK を中断します。
- MSI X WDK ネットワーク、割り込みの登録を解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02627f2084f59631c1e1cbf7e443a0a61ab7ef84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374786"
---
# <a name="registering-and-deregistering-an-msi-interrupt"></a>MSI 割り込みの登録および登録解除





ミニポート ドライバーの呼び出しの MSI サポートを登録する、 [ **NdisMRegisterInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterinterruptex) MSI 割り込みを登録する関数。 ドライバーは、初期化、 [ **NDIS\_ミニポート\_割り込み\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics)割り込み特性を指定する構造体と関数のエントリ ポイント。 ドライバーを設定する必要があります、 **MsiSupported** NDIS のメンバー\_ミニポート\_INTERRUPT\_特性構造体を**TRUE**します。 ドライバーは、構造体を渡します**NdisMRegisterInterruptEx**します。

割り込みの MSI をサポートするには、次の関数を定義する必要があります。

-   [*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt)

-   [*MiniportMessageInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt_dpc)

-   [*MiniportDisableMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_disable_message_interrupt)

-   [*MiniportEnableMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_enable_message_interrupt)

ミニポート ドライバーがドライバーには、MSI のエントリ ポイントがサポートしている場合でも、(これは、次のリストに表示されます) の行に基づく割り込み関数では、エントリ ポイントを提供する必要があります。 NDIS が、MSI の割り込みを与えない場合は、フォールバックの条件として標準割り込みを付与ができます。

行の割り込み関数を以下に示します。

-   [*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)

-   [*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)

-   [*MiniportDisableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_disable_interrupt)

-   [*MiniportEnableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_enable_interrupt)

ドライバーを呼び出す必要があります、 [ **NdisMDeregisterInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)関数で以前に割り当てられたリソースを解放する**NdisMRegisterInterruptEx**します。

 

 





