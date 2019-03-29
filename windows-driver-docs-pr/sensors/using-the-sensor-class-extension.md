---
title: センサー クラスの拡張機能の使用
description: センサー クラスの拡張機能には、センサー ドライバーとセンサー API の間のリンケージがサポートしています。
ms.assetid: F9632F86-10E8-4006-8FB7-97FA5EED492D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10b4818e8e7da6513df09adffb1fe2a1abf8db0e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580429"
---
# <a name="using-the-sensor-class-extension"></a>センサー クラスの拡張機能の使用


センサー クラスの拡張機能には、センサー ドライバーとセンサー API の間のリンケージがサポートしています。

センサー アプリケーションは、ドライバーからのイベント通知を受信登録することによって、ADXL345 データ フィールドを取得するは。 アプリケーションは、データ更新イベントの登録をした後、ドライバーは、センサーからデータを受信するたびにこれらのイベントを生成します。 これらのイベント通知の頻度は、現在のレポート間隔プロパティに対応します。

ドライバーを起動すると、 **ISensorClassExtension::PostEvent**メソッド内から、 **CSensorDdi::PostDataEvent**センサー api メソッド、クラス拡張は転送通知します。 ドライバーのサンプルでは、イベント、スレッドをサポートします。 このスレッドに関連付けられているコードでは、センサーからのデータ更新を受信し、により、ドライバーが、指定したレポート間隔でデータを送信しています。 このコードを呼び出す、 **CSensorDdi::ReportIntervalExpired** 、によって実行されるメソッド、 **PostDataEvent**メソッド。

## <a name="related-topics"></a>関連トピック
[SpbAccelerometer ドライバーのサンプル](spbaccelerometer-driver-sample.md)  
[I/O ドライバー モデル](the-driver-i-o-model.md)  



