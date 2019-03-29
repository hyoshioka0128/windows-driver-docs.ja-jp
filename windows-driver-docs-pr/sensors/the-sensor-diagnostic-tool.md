---
title: センサー診断ツールを使用したセンサー機能をテストします。
description: センサー診断ツールを使用すると、ドライバー、ファームウェア、およびハードウェアの機能をテストできます。
ms.assetid: 447E1348-53BA-4AD4-9010-A6452F46A827
keywords:
- センサーのテスト
- テストのセンサー
- センサー診断ツール
- センサーのドライバーのテスト
- センサーのファームウェアのテスト
- センサーのハードウェアのテスト
- センサー イベント
- センサー、レポート間隔
- センサー、感度の変更
- レポート間隔
- 感度を変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9436c96016c702efdc95c1fe32919b7d6b4b6dce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580332"
---
# <a name="testing-sensor-functionality-with-the-sensor-diagnostic-tool"></a>センサー診断ツールを使用したセンサー機能をテストします。


センサー診断ツールを使用すると、ドライバー、ファームウェア、およびハードウェアの機能をテストできます。

ツールは、テストするには、Sensor and Location API を呼び出します。

-   データの取得
-   イベント処理
-   レポート間隔
-   感度を変更します。
-   プロパティの取得

これらのテストを実行するアプリケーションを作成する代わりには、Windows Driver Kit (WDK) の一部として出荷されるセンサー診断ツールを使用することができます。

たとえば、ドライバー開発用コンピューターは x64 ベースのマシンでは、既定の場所に WDK をインストールした場合は、次のフォルダーにセンサー診断ツールが検索されます。

*C:\\Program Files (x86)\\Windows キット\\10\\ツール\\x64\\sensordiagnostictool.exe*センサーまたは場所のドライバーがインストールされると、ハードウェアアタッチされている pc に、ツールすぐに認識され、記録、デバイスで使用可能なセンサーの一覧。

次の図は、いくつかのセンサーが PC に接続しているときに、センサー診断ツールの起動画面を示します。 左側のウィンドウで、PC で使用可能なセンサーが表示されます。

![センサー診断ツール: スタートアップ](images/sdt-startup.png)

この場合、センサー診断ツールでは、一連の HID センサーだけでなく、シンプルなデバイスの向きのセンサー、Windows 位置と地理的位置情報ドライバー サンプルでサポートされている地理的位置情報センサーの存在が検出されました。

## <a name="support-for-ambient-light-sensors"></a>環境光センサーのサポート


センサー診断ツールには、環境光センサー (ALS) のサポートが含まれています。 現在のディスプレイの明るさは、ツールの左上隅で、SB % ボックスで報告されます。

ただしがツールが ALS 値を取得する場合は、これらの値として返すことに注意してください (LUX、オフセット) のペア。 この順序は、Advanced Configuration and Power Interface (ACPI) (オフセット、LUX) の標準のペアによって異なります。

## <a name="related-topics"></a>関連トピック
[センサーの機能をテストします。](testing-sensor-functionality.md)  
[場所の機能をテストします。](testing-location-functionality.md)  



