---
title: パラレル ポートに接続されているパラレル デバイスの操作
description: パラレル ポートに接続されているパラレル デバイスの操作
ms.assetid: 5ad36162-efbe-4be8-954c-964ef12c539a
keywords:
- パラレルポート WDK、並列デバイス操作
- パラレルデバイス WDK
- ベンダー提供のパラレルドライバー WDK、パラレルデバイス操作
- パラレルデバイス WDK、クライアント操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57cc0f91fbf5673e879308d7c81a43661cf2b643
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844493"
---
# <a name="operating-a-parallel-device-attached-to-a-parallel-port"></a>パラレル ポートに接続されているパラレル デバイスの操作





このセクションでは、クライアント (特に、並列デバイス用のベンダーが提供する関数ドライバー) がパラレルポートに接続されている並列デバイスを操作する方法について説明します。

パラレルポートに対してシステム指定のバスドライバーを使用すると、パラレルポートで列挙された各並列デバイス用に物理デバイスオブジェクト (PDO) が作成されます。 次のトピックでは、デバイスの PDO によって提供されるインターフェイスを使用して、クライアントが並列デバイスを操作する方法について説明します。

[並列デバイスを開いて使用する](opening-and-using-a-parallel-device.md)

[パラレルデバイスへの接続](connecting-to-a-parallel-device.md)

[パラレルデバイスに関する情報の取得](obtaining-information-about-a-parallel-device.md)

[並列デバイスで使用するためのパラレルポートのロックとロック解除](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

[パラレルデバイスの通信モードの設定とクリア](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

[パラレルデバイスでの属性の設定](setting-attributes-on-a-parallel-device.md)

[並列デバイスの読み取りと書き込み](reading-and-writing-a-parallel-device.md)

パラレルポートに接続されている並列デバイスのサポートの詳細については、以下を参照してください。

[ParallelPorts とデバイスの概要](introduction-to-parallel-ports-and-devices.md)

[システム提供のパラレル ドライバー](system-supplied-parallel-drivers.md)

[システム提供のパラレルドライバーへのクライアントインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 




