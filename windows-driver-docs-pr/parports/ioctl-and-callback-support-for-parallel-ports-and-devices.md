---
title: パラレル ポートとデバイスの IOCTL とコールバックのサポート
description: パラレル ポートとデバイスの IOCTL とコールバックのサポート
ms.assetid: 72a31f50-2f59-4a4d-aac7-571f83a94259
keywords:
- システム提供平行ドライバー WDK、Ioctl
- Ioctl WDK 並列ドライバー
- コールバック WDK 並列ドライバー
- システム提供平行ドライバー WDK、コールバック
- WDK、コールバックをデバイスに並列します。
- デバイス、WDK の Ioctl に並列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8d707bbd2b70b5af8ce580c5ba9ab489eceff6d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373532"
---
# <a name="ioctl-and-callback-support-for-parallel-ports-and-devices"></a>パラレル ポートとデバイスの IOCTL とコールバックのサポート





このセクションでは、システム提供平行ドライバーがオペレーティング パラレル ポートおよびパラレル ポートに接続されたデバイスをサポートする方法を説明するトピックへのリンクを提供します。

パラレル ポートに接続されている並列のデバイスのベンダー関数ドライバーは省略可能です。 システム提供平行ドライバー提供広範なサポート、ロウ デバイスとしての並列のデバイスを直接制御するため、デバイスの親を操作するためにパラレル ポート。

については、システムによって提供される関数のドライバーには、Ioctl とコールバックにパラレル ポートを操作するには、次のトピックでは、参照してください。

[パラレル ポートに関する情報の取得](obtaining-information-about-a-parallel-port.md)

[パラレル ポートの使用を同期します。](synchronizing-the-use-of-a-parallel-port.md)

[選択して、パラレル ポートに接続されている IEEE 1284 デバイスの選択を解除](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

[設定およびパラレル ポートの通信モードを解除](setting-and-clearing-the-communication-mode-on-a-parallel-port.md)

[1284.3 データ、IEEE に接続するデバイスをリンクします。](connecting-to-an-ieee-1284-3-data-link-device.md)

Ioctl およびパラレル ポートに接続されている並列のデバイスを操作するシステム提供のバス ドライバーを提供するコールバックについては、次を参照してください。

[起動と使用の並列のデバイス](opening-and-using-a-parallel-device.md)

[並列デバイスへの接続](connecting-to-a-parallel-device.md)

[並列デバイスに関する情報を取得します。](obtaining-information-about-a-parallel-device.md)

[ロックおよび並列のデバイスで使用するため、パラレル ポートのロックを解除](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

[設定および並列のデバイスの通信モードを解除](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

[並列のデバイスに属性を設定](setting-attributes-on-a-parallel-device.md)

[並列のデバイスの読み取りと書き込み](reading-and-writing-a-parallel-device.md)

パラレル ポートおよびパラレル ポートに接続されたデバイスが動作する方法の詳細についてを参照してください。

[パラレル ポートの動作](operating-a-parallel-port.md)

[パラレル ポートに接続されている並列のデバイスの動作](operating-a-parallel-device-attached-to-a-parallel-port.md)

[システム提供平行ドライバーへのクライアント インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543926)

 

 




