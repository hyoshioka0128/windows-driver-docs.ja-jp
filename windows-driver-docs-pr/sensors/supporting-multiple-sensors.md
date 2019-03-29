---
title: 複数のセンサーをサポートしています。
description: SpbAccelerometer サンプルでは、1 つのセンサー デバイス用のドライバーを記述する方法を示します。
ms.assetid: 633B7CB5-EF4A-42BE-A60E-7D12BDAFA34F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05876f4790b01a2589c92e1bafab2809b599ad7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580945"
---
# <a name="supporting-multiple-sensors"></a>複数のセンサーをサポートしています。


SpbAccelerometer サンプルでは、1 つのセンサー デバイス用のドライバーを記述する方法を示します。 ただし、クラス拡張のセンサーおよびセンサー DDI には、複数のセンサー デバイスに対応します。 複数のセンサーをサポートするために、サンプル ドライバーには、次の変更を検討してください。

SensorDdi を 2 つのクラスに分割します。

1.  SensorDdi
2.  センサー

実装することで、センサー クラスの拡張機能との通信を容易に SensorDdi クラスは引き続き、 **ISensorDriver**インターフェイス、および呼び出しを使用して、 **ISensorClassExtension**インターフェイスです。 このクラスは、センサー ID 文字列によってインデックス付けされた、現在のセンサーのリストを保持もする必要があります。

各センサーでは、新しいセンサー クラスのインスタンスを作成します。 このクラスが維持されます。 状態、プロパティ、およびデータ フィールド。 各センサーのインスタンスは、独自の ClientManager と ReportManager もあります。

センサー DDI のコールバックのいずれかを受け取ると、SensorDDI クラスはセンサー ID と一致し、適切なセンサー インスタンスに対応するメソッドを呼び出します。

次の図の左側にあるダウンロード時に存在する場合、ドライバーのサンプルを示しています。 図の右側にあるを示し、このドライバーのこのトピック内の変更が適用された後に 2 つ目のデバイスのサポートが追加されました。

![複数のセンサーのサポート](images/multi-sensor.png)

 

 




