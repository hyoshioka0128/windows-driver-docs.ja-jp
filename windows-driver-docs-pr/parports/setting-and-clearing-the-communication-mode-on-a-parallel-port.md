---
title: パラレル ポートの通信モードの設定と解除
description: パラレル ポートの通信モードの設定と解除
ms.assetid: a22cdeef-4ae7-49f8-b0b5-a4d68feb4235
keywords:
- パラレル ポート WDK、通信モード
- WDK パラレル ポートの通信モード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cd24e2f6a3a76d90ead670c548043c08e665474
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358467"
---
# <a name="setting-and-clearing-the-communication-mode-on-a-parallel-port"></a>パラレル ポートの通信モードの設定と解除





クライアントは、次の内部デバイス制御要求を使用してパラレル ポートの通信モードを設定します。

[**IOCTL\_内部\_並列\_設定\_チップ\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parallel_set_chip_mode)

[**IOCTL\_内部\_並列\_クリア\_チップ\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parallel_clear_chip_mode)

カーネル モード ドライバーは、システム提供も使用できます[デバイス コールバック ルーチンを並列](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)で取得した、 [ **IOCTL\_内部\_取得\_並列\_PNP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)要求。 この要求を返します、 [**並列\_PNP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ns-parallel-_parallel_pnp_information)システム提供のコールバックに次のポインターを含む構造体。

-   **TrySetChipMode**メンバーがへのポインターを[ *PPARALLEL\_設定\_チップ\_モード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_set_chip_mode)コールバックで、オペレーティング システムの設定パラレル ポートのモードです。

-   **ClearChipMode**メンバーへのポインターを[ *PPARALLEL\_クリア\_チップ\_モード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_clear_chip_mode)コールバックをクリアしますIEEE 1284 互換モードにホスト チップセットの通信モードをリセットしてパラレル ポートの動作モード。

クライアント設定、通信モードをオフにする前にパラレル ポートが最初に割り当てる必要があります。

新しい通信モードを設定できます前に、クライアントは通信モードを解除最初にする必要があります。 通信モードをオフにすると、ホスト チップセットが IEEE 1284 互換モードを返します。

現在のモードを確認するのには、クライアントが、IOCTL を使用できる\_内部\_取得\_並列\_PNP\_情報の要求は、並列を返します\_PNP\_情報現在の通信モードに関する情報を含む構造体。

 

 




