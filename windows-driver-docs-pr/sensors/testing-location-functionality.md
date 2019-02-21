---
title: 場所の機能をテストします。
description: センサー診断ツールには、ログの場所に固有のプロパティ、別の場所 タブが含まれています。
ms.assetid: A96AF9C7-69FA-492C-941E-4E296488875C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8684ac12c530cebc1c25e08f58b5a1e5d9abd5c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558101"
---
# <a name="testing-location-functionality"></a>場所の機能をテストします。


センサー診断ツールには、ログの場所に固有のプロパティ、別の場所 タブが含まれています。 これらのプロパティには、緯度、経度、および都市の住所が含まれます。

>[!NOTE]
> センサー診断ツールは Windows 8.1 およびそれ以前のオペレーティング システムでのテストに使用できます。 Windows 10 用ツールが非推奨となりましたのでセンサー ドライバーのテストと Windows 10 以降のオペレーティング システムでの診断は、使用してください SensorInfo アプリ、Microsoft Store から。



## <a name="configuring-the-sensor-diagnostic-tool-to-capture-location-data"></a>場所データをキャプチャするセンサー診断ツールを構成します。


次の手順では、Windows の場所プロバイダーのイベントをキャプチャするセンサー診断ツールを構成する方法について説明します。

1.  センサーの左側のウィンドウで、Windows の場所プロバイダーのノードを展開し、確認、**接続**と**サブスクライブ済み**ボックス。
2.  Windows 位置情報取得のノードをクリックします。

ノードをクリックした後、**プロパティ**と**データ**場所データの右側のウィンドウでタブを更新します。

## <a name="tracking-location-data"></a>場所データの追跡


使用して特定のプロパティとデータの表示を開始するには (このトピックでは、前のセクションを参照してください)、場所データをキャプチャするセンサー診断ツールを構成した後、**場所**タブ。

1.  開く、**場所**タブ。
2.  緯度と経度の値を表示するには、左側のウィンドウの LatLong ノードをクリックします。
3.  都市の住所を表示するには、左側のウィンドウで CivicAddress ノードをクリックします。

## <a name="related-topics"></a>関連トピック
[センサー診断ツール](the-sensor-diagnostic-tool.md)
[センサー機能をテストします。](testing-sensor-functionality.md)



