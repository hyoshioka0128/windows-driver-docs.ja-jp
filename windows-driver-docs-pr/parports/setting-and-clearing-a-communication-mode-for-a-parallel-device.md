---
title: パラレル デバイスの通信モードの設定と解除
description: パラレル デバイスの通信モードの設定と解除
ms.assetid: 2ff53ed0-dbb7-4c8f-b6e4-5f7d20124a7c
keywords:
- パラレルデバイス WDK、通信モード
- 通信モード WDK の並列デバイス
- 通信モードのクリア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7abc68f65e1a9076251efdb33ed57d8dd4282ee3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842322"
---
# <a name="setting-and-clearing-a-communication-mode-for-a-parallel-device"></a>パラレル デバイスの通信モードの設定と解除





クライアントは、次のデバイス制御要求を使用して、並列デバイスの通信モードを設定できます。

-   [**IOCTL\_IEEE1284\_GET\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_get_mode)は、デバイスで設定されている現在の通信プロトコルを返します。 この要求を使用するには、ポートをロックする必要はありません。

-   [**IOCTL\_IEEE1284\_NEGOTIATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate)は、新しい通信モードをネゴシエートします。 パラレルポートが割り当てられ、IEEE 1284.3 デバイスが選択されている必要があります。

-   [**IOCTL\_内部\_切断\_アイドル状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_disconnect_idle)になると、通信モードが IEEE\_互換に設定されます。 パラレルポートが割り当てられ、IEEE 1284.3 デバイスが選択されている必要があります。

カーネルモードドライバーは、システムによって提供される[並列デバイスコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用することもできます。 [**IOCTL\_内部\_parclass\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_connect)要求は、システム提供のコールバックルーチンへの次のポインターを含む[**PARCLASS\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parclass_information)構造体を返します。

-   決定**Eieeemode**メンバーは、 [**pdetermine\_ieee\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pdetermine_ieee_modes)のコールバックへのポインターであり、パラレルポートがサポートする ieee 通信モードを決定します。

-   **NegotiateIeeeMode**メンバーは、 [**PNEGOTIATE\_IEEE\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pnegotiate_ieee_mode)コールバックへのポインターであり、パラレルポートバスドライバーが呼び出し元によって指定されたモード間でサポートする最速の ieee 通信モードを設定します。

-   **TerminateIeeeMode**メンバーは、 [**pterminate\_ieee\_mode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pterminate_ieee_mode)コールバックへのポインターであり、通信モードを ieee 1284 互換モードに設定します。

-   **Ieeefwdtorev**メンバーは[ **\_REV コールバックへの PPARALLEL\_IEEE\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_ieee_fwd_to_rev)へのポインターです。これにより、データ転送方向が転送から反転 (書き込みから読み取り) に変更されます。

-   **Ieeerevtofwd**メンバーは、高速コールバック[**を\_するための PPARALLEL\_IEEE\_REV\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_ieee_rev_to_fwd)へのポインターであり、転送方向を逆方向 (読み取りから書き込み) に変更します。

パラレルポートバスドライバーでサポートされている通信モードの詳細については、Windows Driver Kit (WDK) のヘッダーファイル*ntddpar*に定義されているいずれかのモードの [\_ECP 以外] を参照してください。

 

 




