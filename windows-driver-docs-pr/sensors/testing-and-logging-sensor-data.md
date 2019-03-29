---
title: センサーのプロパティ サポートのテスト
description: センサー診断ツールを使用すると、ドライバーとファームウェア プロパティの取得をサポートしているかどうかをテストできます。
ms.assetid: 6E8C2162-F7BD-4544-8869-00FA4E4925E0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f198099827ed031451116d864c2b1f0894ddb464
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577938"
---
# <a name="testing-sensor-property-support"></a>センサーのプロパティ サポートのテスト


センサー診断ツールを使用すると、ドライバーとファームウェア プロパティの取得をサポートしているかどうかをテストできます。 このツールでは、プロパティの取得をサポートするかどうかを判断するセンサー API でのプロパティを呼び出します。
 

## <a name="configuring-the-sensor-diagnostic-tool-to-retrieve-sensor-properties"></a>センサーのプロパティを取得するセンサー診断ツールを構成します。


加速度計のプロパティを取得できるように、診断のツールを構成するには、次の操作を行います。

1.  加速度計センサーの左側のウィンドウでのノードを展開し、確認、**接続**ボックス。
2.  センサーの左側のウィンドウで、加速度計ノードをクリックします。

右側のウィンドウの [プロパティ] セクションには、センサーの更新されたプロパティのデータが含まれています。 このデータは、デバイスでサポートされるプロパティに対応します。

[センサー イベントのテスト](testing-sensor-events.md)トピックでは、ドライバーとファームウェアが感度の変更と、現在のレポート間隔をサポートするかどうかをテストする方法を説明します。 これらのセクションでは、ツールを使用して、プロパティのサポートをテストするときに、これらの設定を変更する方法を理解するを参照してください。

## <a name="related-topics"></a>関連トピック
[センサーの機能をテストします。](testing-sensor-functionality.md)  
[テストのセンサー データの取得](testing-sensor-properties.md)  
[テストのセンサー イベント](testing-sensor-events.md)  



