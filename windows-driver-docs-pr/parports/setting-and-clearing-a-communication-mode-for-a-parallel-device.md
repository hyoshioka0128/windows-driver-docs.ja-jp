---
title: パラレル デバイスの通信モードの設定と解除
description: パラレル デバイスの通信モードの設定と解除
ms.assetid: 2ff53ed0-dbb7-4c8f-b6e4-5f7d20124a7c
keywords:
- デバイスの通信モード、WDK を並列します。
- WDK の並列のデバイスの通信モード
- 通信モードをオフにすると
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bda0a990fd77a8309fc93129db92dd54ba1e5a0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358477"
---
# <a name="setting-and-clearing-a-communication-mode-for-a-parallel-device"></a>パラレル デバイスの通信モードの設定と解除





クライアントは、次のデバイス制御要求を使用して並列のデバイスの通信モードを設定できます。

-   [**IOCTL\_IEEE1284\_取得\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_ieee1284_get_mode)デバイスの設定の現在の通信プロトコルを返します。 ポートを使用して、この要求にロックする必要はありません。

-   [**IOCTL\_IEEE1284\_ネゴシエート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate)新しい通信モードをネゴシエートします。 パラレル ポートを割り当てる必要があるし、IEEE 1284.3 デバイスを選択します。

-   [**IOCTL\_内部\_切断\_IDLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_disconnect_idle) IEEE 通信モードに設定\_互換性。 パラレル ポートを割り当てる必要があるし、IEEE 1284.3 デバイスを選択します。

カーネル モード ドライバーは、システム提供も使用できます[デバイス コールバック ルーチンを並列](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 [ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parclass_connect)を返します要求を[ **PARCLASS\_情報。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ns-parallel-_parclass_information)システム提供のコールバック ルーチンに次のポインターを含む構造体。

-   **DetermineIeeeMode**メンバーがへのポインター、 [ **PDETERMINE\_IEEE\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pdetermine_ieee_modes)コールバックで、IEEE の通信を決定します。パラレル ポートをサポートするモード。

-   **NegotiateIeeeMode**メンバーがへのポインター、 [ **PNEGOTIATE\_IEEE\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pnegotiate_ieee_mode)コールバックで、最速の IEEE 通信の設定呼び出し元によって指定されたモードの中から、パラレル ポート バス ドライバーをサポートするモード。

-   **TerminateIeeeMode**メンバーがへのポインター、 [ **PTERMINATE\_IEEE\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pterminate_ieee_mode)コールバックは、IEEE に通信モードを設定します。1284 互換モード。

-   **IeeeFwdToRev**メンバーがへのポインター、 [ **PPARALLEL\_IEEE\_FWD\_TO\_REV** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_ieee_fwd_to_rev)コールバックデータ転送の方向を逆 (からへの読み取り書き込み) に順方向から変更します。

-   **IeeeRevToFwd**メンバーがへのポインター、 [ **PPARALLEL\_IEEE\_REV\_TO\_FWD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_ieee_rev_to_fwd)コールバックリバース (から読み取り、書き込み) を転送する転送の方向を変更します。

パラレル ポート バス ドライバーがサポートする通信モードの詳細については、ECP を通じて NONE モードを参照してください。\_ヘッダー ファイルで定義されている ANY *ntddpar.h* Windows Driver Kit (WDK) にします。

 

 




