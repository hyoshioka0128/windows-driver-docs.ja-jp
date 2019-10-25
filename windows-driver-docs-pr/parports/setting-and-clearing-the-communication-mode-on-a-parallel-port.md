---
title: パラレル ポートの通信モードの設定と解除
description: パラレル ポートの通信モードの設定と解除
ms.assetid: a22cdeef-4ae7-49f8-b0b5-a4d68feb4235
keywords:
- パラレルポート WDK、通信モード
- 通信モード WDK パラレルポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97c4604b81457f816a4051ada91ccaa2a322e226
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842320"
---
# <a name="setting-and-clearing-the-communication-mode-on-a-parallel-port"></a>パラレル ポートの通信モードの設定と解除





クライアントは、次の内部デバイス制御要求を使用して、パラレルポートで通信モードを設定します。

[**IOCTL\_内部\_並列\_チップ\_モード\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_set_chip_mode)

[**IOCTL\_内部\_並列\_チップ\_モードをクリア\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_clear_chip_mode)

また、カーネルモードドライバーでは、システムによって提供される[並列デバイスコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用することもできます。このルーチンは、 [**IOCTL\_内部\_\_パラレル\_PNP\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)要求を取得します。 この要求は、システムによって提供されるコールバックへの次のポインターを含む、[**パラレル\_PNP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_pnp_information)構造体を返します。

-   **TrySetChipMode**メンバーは、パラレルポートの動作モードを設定する[*PPARALLEL\_セット\_チップ\_モード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_set_chip_mode)コールバックへのポインターです。

-   **ClearChipMode**メンバーは、 [*PPARALLEL\_CLEAR\_チップ\_モード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_clear_chip_mode)コールバックへのポインターであり、ホストチップの通信モードを IEEE 1284-compatibility にリセットすることによってパラレルポートの動作モードをクリアします。mode.

クライアントは、通信モードを設定またはクリアする前に、まずパラレルポートを割り当てる必要があります。

クライアントは、新しい通信モードを設定する前に、最初に通信モードをクリアする必要があります。 通信モードをオフにすると、ホストチップセットが IEEE 1284 互換モードに戻ります。

現在のモードを確認するために、クライアントは IOCTL\_内部\_GET\_PARALLEL\_PNP\_INFO 要求を使用できます。これにより、この要求は、現在の通信モード。

 

 




