---
title: パラレル デバイスへの接続
description: パラレル デバイスへの接続
ms.assetid: c05a1a1e-308a-4b9f-af43-761c4c14d6af
keywords:
- デバイス接続、WDK を並列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8aa8e7076f59f93b6168b6204ec5e2b439f4d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582586"
---
# <a name="connecting-to-a-parallel-device"></a>パラレル デバイスへの接続





クライアントを使用して、 [ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff544040)を取得する要求を[ **PARCLASS\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544334)を含む構造体。

-   パラレル ポートに割り当てられている I/O リソース

-   パラレル ポートのハードウェア機能

-   並列のデバイスでの IEEE 1284 動作モードを設定する、カーネル モード ドライバーが使用できるコールバック ルーチンへのポインターを参照してください[設定および並列のデバイスの通信モードを解除](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

-   カーネル モード ドライバーが読み取りと書き込みの並列のデバイスで使用できるコールバック ルーチンへのポインターを参照してください[並列デバイスの読み書き](reading-and-writing-a-parallel-device.md)します。

コールバック ルーチンは、関数の一般的なドライバーが必要な機能を提供します。 コールバック ルーチンを使用すると、同等のデバイスに対する制御要求を使用するよりも効率的です。

使用して、クライアントがデバイスから切断する[ **IOCTL\_内部\_PARCLASS\_切断**](https://msdn.microsoft.com/library/windows/hardware/ff544046)要求。

 

 




