---
title: パラレル ポートの操作
description: パラレル ポートの操作
ms.assetid: c9015a01-a7cb-41f4-9710-a868ef19f6d7
keywords:
- ベンダー提供のパラレルドライバー WDK、パラレルポート操作
- システム提供の関数ドライバー WDK パラレルポート
- 関数ドライバー WDK のパラレルポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 994070744393cc3ed89e463336f947277367415d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842736"
---
# <a name="operating-a-parallel-port"></a>パラレル ポートの操作





このセクションでは、クライアント (特に、並列デバイス用のベンダーが提供する関数ドライバー) がパラレルポートを操作する方法について説明します。

システムによって提供されるパラレルポートの関数ドライバーは、システム内で列挙された各パラレルポートに対して機能デバイスオブジェクト (FDO) を作成します。 次のトピックでは、ポートの FDO によって提供されるインターフェイスを使用して、クライアントがパラレルポートを操作する方法について説明します。

[パラレルポートの作成と開始](creating-and-starting-a-parallel-port.md)

[パラレルポートを開いたり閉じたりする](opening-and-closing-a-parallel-port.md)

[パラレルポートに関する情報の取得](obtaining-information-about-a-parallel-port.md)

[パラレルポートの使用の同期](synchronizing-the-use-of-a-parallel-port.md)

[パラレルポートに接続されている IEEE 1284 デバイスの選択と選択解除](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

[パラレルポートでの通信モードの設定とクリア](setting-and-clearing-the-communication-mode-on-a-parallel-port.md)

[IEEE 1284.3 データリンクデバイスへの接続](connecting-to-an-ieee-1284-3-data-link-device.md)

[割り込みサービスルーチンをパラレルポートに接続する](connecting-an-interrupt-service-routine-to-a-parallel-port.md)

パラレルポートのシステムサポートの詳細については、以下を参照してください。

[ParallelPorts とデバイスの概要](introduction-to-parallel-ports-and-devices.md)

[システム提供のパラレル ドライバー](system-supplied-parallel-drivers.md)

[システム提供のパラレルドライバーへのクライアントインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 




