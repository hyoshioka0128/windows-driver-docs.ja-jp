---
title: センサー DDSI 関数
description: センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) 関数では、センサー ドライバーは、クラスの拡張機能との対話を使用してインターフェイスを表します。
ms.assetid: 3DB30155-8DBE-4AE9-A0CC-8089DC255E32
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0afbf379b21e98378e19cf552ca99cffa61b5a70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571963"
---
# <a name="sensor-ddsi-functions"></a>センサー DDSI 関数

センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) 関数では、センサー ドライバーは、クラスの拡張機能との対話を使用してインターフェイスを表します。 これらの関数は、クラスの拡張機能によって実装されます。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|---|---|
|SensorsCxDeviceInitConfig|この関数は、センサー デバイスを構成します。|
|SensorsCxDeviceInitialize|この関数では、クラス拡張のセンサーを初期化します。|
|SensorsCxSensorCreate|この関数は、クラスの拡張機能で、センサーのインスタンスを作成します。|
|SensorsCxSensorInitialize|この関数は、センサーの列挙プロパティを設定します。|
|SensorsCxSensorDataReady|この関数は、ドライバーには、データが取得されたクラスの拡張機能を通知します。|
|SensorsCxStateChange|状態の変更を初期化するために使用します。|
|SensorsCxDeviceGetSensorList|この関数は、WDFDEVICE に関連付けられているセンサーのインスタンスの一覧を返します。|
