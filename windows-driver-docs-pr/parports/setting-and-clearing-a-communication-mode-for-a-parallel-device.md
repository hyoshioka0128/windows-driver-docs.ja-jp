---
title: 設定および並列のデバイスの通信モードを解除
description: 設定および並列のデバイスの通信モードを解除
ms.assetid: 2ff53ed0-dbb7-4c8f-b6e4-5f7d20124a7c
keywords:
- デバイスの通信モード、WDK を並列します。
- WDK の並列のデバイスの通信モード
- 通信モードをオフにすると
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a2680d79b405c41a4c6c9f03f42ebb6319e58ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556761"
---
# <a name="setting-and-clearing-a-communication-mode-for-a-parallel-device"></a>設定および並列のデバイスの通信モードを解除





クライアントは、次のデバイス制御要求を使用して並列のデバイスの通信モードを設定できます。

-   [**IOCTL\_IEEE1284\_取得\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff543975)デバイスの設定の現在の通信プロトコルを返します。 ポートを使用して、この要求にロックする必要はありません。

-   [**IOCTL\_IEEE1284\_ネゴシエート**](https://msdn.microsoft.com/library/windows/hardware/ff543978)新しい通信モードをネゴシエートします。 パラレル ポートを割り当てる必要があるし、IEEE 1284.3 デバイスを選択します。

-   [**IOCTL\_内部\_切断\_IDLE** ](https://msdn.microsoft.com/library/windows/hardware/ff543993) IEEE 通信モードに設定\_互換性。 パラレル ポートを割り当てる必要があるし、IEEE 1284.3 デバイスを選択します。

カーネル モード ドライバーは、システム提供も使用できます[デバイス コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544275)します。 [ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff544040)を返します要求を[ **PARCLASS\_情報。**](https://msdn.microsoft.com/library/windows/hardware/ff544334)システム提供のコールバック ルーチンに次のポインターを含む構造体。

-   **DetermineIeeeMode**メンバーがへのポインター、 [ **PDETERMINE\_IEEE\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff544365)コールバックで、IEEE の通信を決定します。パラレル ポートをサポートするモード。

-   **NegotiateIeeeMode**メンバーがへのポインター、 [ **PNEGOTIATE\_IEEE\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff544386)コールバックで、最速の IEEE 通信の設定呼び出し元によって指定されたモードの中から、パラレル ポート バス ドライバーをサポートするモード。

-   **TerminateIeeeMode**メンバーがへのポインター、 [ **PTERMINATE\_IEEE\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff544773)コールバックは、IEEE に通信モードを設定します。1284 互換モード。

-   **IeeeFwdToRev**メンバーがへのポインター、 [ **PPARALLEL\_IEEE\_FWD\_TO\_REV** ](https://msdn.microsoft.com/library/windows/hardware/ff544524)コールバックデータ転送の方向を逆 (からへの読み取り書き込み) に順方向から変更します。

-   **IeeeRevToFwd**メンバーがへのポインター、 [ **PPARALLEL\_IEEE\_REV\_TO\_FWD** ](https://msdn.microsoft.com/library/windows/hardware/ff544528)コールバックリバース (から読み取り、書き込み) を転送する転送の方向を変更します。

パラレル ポート バス ドライバーがサポートする通信モードの詳細については、ECP を通じて NONE モードを参照してください。\_ヘッダー ファイルで定義されている ANY *ntddpar.h* Windows Driver Kit (WDK) にします。

 

 




