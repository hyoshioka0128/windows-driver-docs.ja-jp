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
ms.openlocfilehash: 648b059770ad572720b9f95a40e573d0eb4d1a06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574783"
---
# <a name="registering-and-deregistering-an-msi-interrupt"></a>MSI 割り込みの登録および登録解除





ミニポート ドライバーの呼び出しの MSI サポートを登録する、 [ **NdisMRegisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563649) MSI 割り込みを登録する関数。 ドライバーは、初期化、 [ **NDIS\_ミニポート\_割り込み\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566465)割り込み特性を指定する構造体と関数のエントリ ポイント。 ドライバーを設定する必要があります、 **MsiSupported** NDIS のメンバー\_ミニポート\_INTERRUPT\_特性構造体を**TRUE**します。 ドライバーは、構造体を渡します**NdisMRegisterInterruptEx**します。

割り込みの MSI をサポートするには、次の関数を定義する必要があります。

-   [*MiniportMessageInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559407)

-   [*MiniportMessageInterruptDpc*](https://msdn.microsoft.com/library/windows/hardware/ff559411)

-   [*MiniportDisableMessageInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559376)

-   [*MiniportEnableMessageInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559383)

ミニポート ドライバーがドライバーには、MSI のエントリ ポイントがサポートしている場合でも、(これは、次のリストに表示されます) の行に基づく割り込み関数では、エントリ ポイントを提供する必要があります。 NDIS が、MSI の割り込みを与えない場合は、フォールバックの条件として標準割り込みを付与ができます。

行の割り込み関数を以下に示します。

-   [*MiniportInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559395)

-   [*MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)

-   [*MiniportDisableInterruptEx*](https://msdn.microsoft.com/library/windows/hardware/ff559375)

-   [*MiniportEnableInterruptEx*](https://msdn.microsoft.com/library/windows/hardware/ff559380)

ドライバーを呼び出す必要があります、 [ **NdisMDeregisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563575)関数で以前に割り当てられたリソースを解放する**NdisMRegisterInterruptEx**します。

 

 





