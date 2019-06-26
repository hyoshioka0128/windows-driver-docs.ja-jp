---
title: ディスプレイ ミニポート ドライバーの初期化
description: ディスプレイ ミニポート ドライバーの初期化
ms.assetid: 505dab48-7c00-4bf4-8433-487360f67b26
keywords:
- 初期化のミニポート ドライバー WDK で表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25d76e164c430840c1c7fe1261a12b79289132c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385190"
---
# <a name="initializing-the-display-miniport-driver"></a>ディスプレイ ミニポート ドライバーの初期化


オペレーティング システムがディスプレイのミニポート ドライバーが読み込まれた後、次の手順は、ディスプレイのミニポート ドライバーを初期化するために発生します。

1.  オペレーティング システムの呼び出し、ディスプレイのミニポート ドライバーの[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)関数。

2.  **DriverEntry**割り当てます、 [**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)構造体し、設定、**バージョン**のメンバードライバー\_初期化\_DXGKDDI を使用してデータ\_インターフェイス\_バージョンとドライバーの残りのメンバー\_初期化\_表示へのポインターを使用してデータミニポート ドライバーの他のエントリ ポイント関数 (ディスプレイのミニポート ドライバーを実装する関数) です。

3.  **DriverEntry**呼び出し、 [ **DxgkInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nf-dispmprt-dxgkinitialize) Microsoft DirectX グラフィックスのカーネルのサブシステムを読み込みます (*Dxgkrnl.sys*) を指定して、DirectX グラフィックスのカーネル サブシステム、ディスプレイのミニポート ドライバーへのポインターでの他のエントリ ポイント関数です。

4.  後**DxgkInitialize**から制御が戻る**DriverEntry**の戻り値を反映**DxgkInitialize**オペレーティング システムに戻したりします。 表示のミニポート ドライバー開発者がいることを値に関する前提条件もありません**DxgkInitialize**を返します。

 





