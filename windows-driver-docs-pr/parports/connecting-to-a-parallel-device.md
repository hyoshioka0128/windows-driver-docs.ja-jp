---
title: パラレル デバイスへの接続
description: パラレル デバイスへの接続
ms.assetid: c05a1a1e-308a-4b9f-af43-761c4c14d6af
keywords:
- デバイス接続、WDK を並列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 117dc1b7831ebbc45070c1d6a65ec84f10c47df0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385985"
---
# <a name="connecting-to-a-parallel-device"></a>パラレル デバイスへの接続





クライアントを使用して、 [ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parclass_connect)を取得する要求を[ **PARCLASS\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ns-parallel-_parclass_information)を含む構造体。

-   パラレル ポートに割り当てられている I/O リソース

-   パラレル ポートのハードウェア機能

-   並列のデバイスでの IEEE 1284 動作モードを設定する、カーネル モード ドライバーが使用できるコールバック ルーチンへのポインターを参照してください[設定および並列のデバイスの通信モードを解除](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

-   カーネル モード ドライバーが読み取りと書き込みの並列のデバイスで使用できるコールバック ルーチンへのポインターを参照してください[並列デバイスの読み書き](reading-and-writing-a-parallel-device.md)します。

コールバック ルーチンは、関数の一般的なドライバーが必要な機能を提供します。 コールバック ルーチンを使用すると、同等のデバイスに対する制御要求を使用するよりも効率的です。

使用して、クライアントがデバイスから切断する[ **IOCTL\_内部\_PARCLASS\_切断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parclass_disconnect)要求。

 

 




