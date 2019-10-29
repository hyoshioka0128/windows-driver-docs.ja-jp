---
title: センサー診断ツールを使用したセンサー機能のテスト
description: センサー診断ツールを使用して、ドライバー、ファームウェア、およびハードウェアの機能をテストします。
ms.assetid: 447E1348-53BA-4AD4-9010-A6452F46A827
keywords:
- センサーのテスト
- センサー, テスト
- センサー診断ツール
- センサードライバー、テスト
- センサーファームウェア、テスト
- センサーハードウェア、テスト
- センサーイベント
- センサー、レポート間隔
- センサー、感度の変更
- レポート間隔
- 感度の変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf429b650ad10d01c4160f2d1dcc0a694216060
ms.sourcegitcommit: f8ef49aa583f63edeab42001af8dfb41031ab622
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72998641"
---
# <a name="testing-sensor-functionality-with-the-sensor-diagnostic-tool"></a>センサー診断ツールを使用したセンサー機能のテスト

> [!IMPORTANT]
> センサー診断ツールは、以前のバージョンの Windows で使用されていました。 サポートされているセンサーのインストールを確認するには、 [Sensorexplorer](https://www.microsoft.com/p/sensorexplorer/9pgl3xpq1tpx?activetab=pivot:overviewtab)を使用することをお勧めします。 

センサー診断ツールを使用して、ドライバー、ファームウェア、およびハードウェアの機能をテストします。

ツールはセンサーと Location API を呼び出して、テストします。

-   データの取得
-   イベント処理
-   レポート間隔
-   感度の変更
-   プロパティの取得

これらのテストを実行するアプリケーションを作成する代わりに、Windows Driver Kit (WDK) の一部として出荷されるセンサー診断ツールを使用できます。

たとえば、ドライバー開発用コンピューターが x64 ベースのコンピューターで、WDK を既定の場所にインストールした場合、センサー診断ツールは次のフォルダーにあります。

*C:\\Program Files (x86)\\Windows キット\\10\\ツール\\x64\\sensordiagnostictool*センサーまたは場所のドライバーがインストールされ、ハードウェアが PC に接続されると、ツールはすぐに使用可能なセンサーの一覧にデバイスを認識して記録します。

次の図は、複数のセンサーが PC に接続されている場合のセンサー診断ツールの起動画面を示しています。 PC で利用可能なセンサーが左側のウィンドウに表示されます。

![センサー診断ツール: スタートアップ](images/sdt-startup.png)

この場合、センサー診断ツールは、HID センサーのコレクション、単純なデバイス指向センサー、Windows ロケーションプロバイダー、および位置情報ドライバーサンプルでサポートされている位置情報センサーの存在を検出しました。

## <a name="support-for-ambient-light-sensors"></a>アンビエント光センサーのサポート

センサー診断ツールには、アンビエント光センサー (ALS) のサポートが含まれています。 現在のディスプレイの明るさは、ツールの左上隅の [SB%] ボックスで報告されます。

ただし、ツールが ALS の値を取得すると、これらの値が (LUX, Offset) のペアとして返される点に注意してください。 この順序は、(オフセット、LUX) ペアの高度な構成と電源インターフェイス (ACPI) 標準とは異なります。

## <a name="related-topics"></a>関連トピック
[センサー機能のテスト](testing-sensor-functionality.md)  
[テスト場所の機能](testing-location-functionality.md)  



