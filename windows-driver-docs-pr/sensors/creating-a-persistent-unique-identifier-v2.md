---
title: ユニバーサルドライバーベースのセンサーの永続的な一意識別子の作成
description: ユニバーサルドライバーベースのドライバーの永続的な一意識別子の作成
ms.assetid: B0131BC5-F76F-46B0-8BDE-4220D971AA29
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2b5cde5f629ad93b38c794dd324da9dcfe050196
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837625"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor"></a>センサーの永続的な一意識別子の作成


ドライバーは、センサーごとに*永続的な一意識別子*(PUID) を作成する必要があります。 PUID は、セッション間で格納され、デバイス上のオブジェクトを一意に識別する GUID 値です。 **DEVPKEY_Sensor_PersistentUniqueId**という名前のプロパティを照会すると、ドライバーは PUID の値を返す必要があります。 デバイスに複数のセンサーが含まれている場合は、各センサーに独自の PUID が割り当てられている必要があります。 アプリケーションでは、この ID を取得するために、 [Windows. デバイス](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)の WinRT api を使用します。

センサーがコンピューターに初めて接続し、後で使用するためにこの値を保存するときに、センサーごとに新しい PUID を作成する必要があります。

ドライバーは、 [SensorsCxSensorInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensorinitialize)初期化ルーチンを呼び出す前に、PUID を作成または取得する必要があります。 この関数は、センサー構成を保持する[SENSOR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_config)構造体へのポインターを提供します。 このポインターを使用して、各デバイスの特定のプロパティストアにアクセスできます。

## <a name="related-topics"></a>関連トピック
[センサードライバーの ADXL345Acc サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617957)
<!--
https://go.microsoft.com/fwlink/p/?LinkId=617957: https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors/ADXL345Acc
-->
