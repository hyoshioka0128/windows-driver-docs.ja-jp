---
title: ディスプレイ ミニポート ドライバーの初期化
description: ディスプレイ ミニポート ドライバーの初期化
ms.assetid: 505dab48-7c00-4bf4-8433-487360f67b26
keywords:
- ミニポートドライバー WDK 表示、初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82e7ca1f2402614a0d7107d4d9855221e9cd1045
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840373"
---
# <a name="initializing-the-display-miniport-driver"></a>ディスプレイ ミニポート ドライバーの初期化


オペレーティングシステムによってディスプレイミニポートドライバーが読み込まれると、次の手順が実行され、ディスプレイミニポートドライバーが初期化されます。

1.  オペレーティングシステムは、ディスプレイミニポートドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)関数を呼び出します。

2.  **Driverentry**は、[**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)構造体を割り当て、ドライバー\_初期化\_データの**バージョン**メンバーを DXGKDDI\_INTERFACE\_version に設定し、ドライバー\_の残りのメンバーは、ディスプレイミニポートドライバーのその他のエントリポイント関数 (または表示ミニポートドライバーが実装する関数) へのポインターを使用して、データ\_初期化します。

3.  **Driverentry**は、 [**Dxgkinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)関数を呼び出して Microsoft DirectX graphics カーネルサブシステム (*Dxgkrnl*) を読み込み、directx グラフィックスカーネルサブシステムにディスプレイミニポートドライバーのその他のエントリへのポインターを提供します。point 関数。

4.  **Dxgkinitialize**が返された後、 **Driverentry**は**dxgkinitialize**の戻り値をオペレーティングシステムに反映します。 表示ミニポートドライバーライターは、 **Dxgkinitialize**が返す値についての前提条件を設定しません。

 





