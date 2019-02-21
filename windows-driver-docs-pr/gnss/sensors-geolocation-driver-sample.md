---
title: Windows 8.1 の地理的位置情報ドライバー サンプル
description: Windows 8.1 用の地理的位置情報サンプル ドライバーでは、グローバル配置 System (GPS) デバイス用センサー ドライバーを示します。
ms.assetid: 2675DB47-B973-419C-930D-1F1B9D65E42D
keywords:
- GPS
- 地理的位置情報ドライバー
- GPS ドライバー
- 無線管理 API
- ラジオ状態の変更
- センサー ドライバー
- UMDF センサー ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1186ad76fdaff67e21e848a074a67d7b4f5af31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528920"
---
# <a name="geolocation-driver-sample-for-windows-81"></a>Windows 8.1 の地理的位置情報ドライバー サンプル

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

Windows 8.1 用の地理的位置情報サンプル ドライバーでは、グローバル配置 System (GPS) デバイス用センサー ドライバーを示します。 このドライバーがハードウェア; に接続できません。それ以外は UMDF センサー ドライバーを構築するためのベスト プラクティスに完全に準拠します。 実際に座標を送信する代わりには、このサンプルは、高度、緯度、経度、およびその他のシミュレートされた GPS データを発行するセンサーをシミュレートします。 さらに、このサンプルは、テストおよびデバッグすると便利であるタイムスタンプを発行します。

このサンプルには、次の 3 つの目的があります。まず、UMDF センサー ドライバーに必要な最小限の機能を示します。 次に、作業用のドライバーを構築するためのスケルトンを提供します。 3 番目に、GPS などのデバイスに対して無線状態の変更通知を提供するオプションの管理 API のサポートが含まれています。

## <a name="related-topics"></a>関連トピック
[センサー診断ツール](https://msdn.microsoft.com/library/windows/hardware/hh780319)  
[場所のセンサー ドライバーの作成](writing-a-location-sensor-driver.md)  
[センサー デバイス ドライバーを作成](https://msdn.microsoft.com/library/windows/hardware/ff545927)  



