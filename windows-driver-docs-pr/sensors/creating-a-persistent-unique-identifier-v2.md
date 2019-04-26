---
title: センサーをベースのユニバーサル ドライバーの永続的な一意の識別子を作成します。
description: ドライバーに基づくユニバーサル ドライバーの永続的な一意の識別子を作成します。
ms.assetid: B0131BC5-F76F-46B0-8BDE-4220D971AA29
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: dec58c2e7626c9848d221e60457ecf6a9bffb3a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359693"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor"></a>センサーの永続的な一意の識別子を作成します。


ドライバーを作成する必要があります、*永続的な一意識別子*(PUID) 各センサーの。 PUID は、セッション間で格納され、デバイス上のオブジェクトを一意に識別する GUID 値です。 ドライバーは、という名前のプロパティに対してクエリを実行時に、PUID の値を返す必要があります**DEVPKEY_Sensor_PersistentUniqueId**します。 デバイスに複数のセンサーが含まれている場合各センサーは、独自の PUID 割り当てる必要があります。 アプリケーションを使用して、この ID を取得することができます、 [Windows.Devices.Enumeration](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) WinRT Api です。

センサーが最初に、コンピューターに接続するときに、各センサーの新しい PUID を作成し、し、後で使用するためには、この値を格納する必要があります。

ドライバーを作成または呼び出しの前に PUID を取得する必要があります、 [SensorsCxSensorInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensorinitialize)初期化ルーチン。 この関数へのポインターを提供する、 [SENSOR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_config)センサーの構成を保持する構造体。 このポインターを使用して、各デバイスの特定のプロパティ ストアにアクセスすることができます。

## <a name="related-topics"></a>関連トピック
[センサー ドライバー ADXL345Acc サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617957)
<!--
https://go.microsoft.com/fwlink/p/?LinkId=617957: https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors/ADXL345Acc
-->
