---
title: ヘッダーの概要-データの分割
description: ヘッダーの概要-データの分割
ms.assetid: ecbf4b08-8be4-42ca-8a65-1cb8124bee33
keywords:
- ヘッダー-データの分割 (WDK)
- ヘッダーとデータを別々のバッファーに分割する
- バッファー WDK ヘッダー-データ分割
- データを受信する WDK ネットワーク
- フレーム WDK ヘッダー-データの分割
- フレームの分割 WDK ヘッダー-データの分割
- storage WDK ヘッダー-データの分割
- スペース management
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0bbe6a27bbf26d2bb40bb0022423e3e7f4088e1
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565682"
---
# <a name="introduction-to-header-data-split"></a>ヘッダーの概要-データの分割

このセクションでは、NDIS 6.1 以降のバージョンで使用できるヘッダーデータ分割サービスについて説明します。 *ヘッダーとデータを分割*すると、受信したイーサネットフレーム内のヘッダーとデータが別々のバッファーに分割されるため、ネットワークのパフォーマンスが向上します。 ヘッダーとデータを分離すると、ヘッダーを1つのメモリ領域にまとめて収集できます。 その結果、より多くのヘッダーが1つのメモリページに格納され、さらに多くのヘッダーがシステムキャッシュに格納されるため、ドライバースタックでのメモリアクセスのオーバーヘッドが削減されます。

このセクションの内容:

[ヘッダーデータの分割の概要](header-data-split-overview.md)

[ヘッダーデータ分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)

[イーサネットフレームの分割](splitting-ethernet-frames.md)

[ヘッダーを使用した通知の受信-データの分割](receive-indications-with-header-data-split.md)

[ヘッダー-データの分割管理と構成](header-data-split-administration-and-configuration.md)

[サポートヘッダー-プロトコルドライバーとフィルタードライバーでのデータの分割](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)

 

 





