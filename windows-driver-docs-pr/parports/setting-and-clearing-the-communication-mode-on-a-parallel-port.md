---
title: 設定およびパラレル ポートの通信モードを解除
description: 設定およびパラレル ポートの通信モードを解除
ms.assetid: a22cdeef-4ae7-49f8-b0b5-a4d68feb4235
keywords:
- パラレル ポート WDK、通信モード
- WDK パラレル ポートの通信モード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be3891065f2b0d765be26f4ab3ed90fface720f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551574"
---
# <a name="setting-and-clearing-the-communication-mode-on-a-parallel-port"></a>設定およびパラレル ポートの通信モードを解除





クライアントは、次の内部デバイス制御要求を使用してパラレル ポートの通信モードを設定します。

[**IOCTL\_内部\_並列\_設定\_チップ\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff544031)

[**IOCTL\_内部\_並列\_クリア\_チップ\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff544017)

カーネル モード ドライバーは、システム提供も使用できます[デバイス コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544275)で取得した、 [ **IOCTL\_内部\_取得\_並列\_PNP\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff543997)要求。 この要求を返します、 [**並列\_PNP\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544299)システム提供のコールバックに次のポインターを含む構造体。

-   **TrySetChipMode**メンバーがへのポインターを[ *PPARALLEL\_設定\_チップ\_モード*](https://msdn.microsoft.com/library/windows/hardware/ff544542)コールバックで、オペレーティング システムの設定パラレル ポートのモードです。

-   **ClearChipMode**メンバーへのポインターを[ *PPARALLEL\_クリア\_チップ\_モード*](https://msdn.microsoft.com/library/windows/hardware/ff544398)コールバックをクリアしますIEEE 1284 互換モードにホスト チップセットの通信モードをリセットしてパラレル ポートの動作モード。

クライアント設定、通信モードをオフにする前にパラレル ポートが最初に割り当てる必要があります。

新しい通信モードを設定できます前に、クライアントは通信モードを解除最初にする必要があります。 通信モードをオフにすると、ホスト チップセットが IEEE 1284 互換モードを返します。

現在のモードを確認するのには、クライアントが、IOCTL を使用できる\_内部\_取得\_並列\_PNP\_情報の要求は、並列を返します\_PNP\_情報現在の通信モードに関する情報を含む構造体。

 

 




