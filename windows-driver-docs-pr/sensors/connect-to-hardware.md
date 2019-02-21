---
title: ハードウェアへの接続します。
description: このトピックでは、センサー ドライバーの割り当てられたハードウェア リソースを決定および I2C ドライバー コント ローラーに接続を示しています。
ms.assetid: 88D9162B-2B99-4608-B31A-48B1810747A9
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4cfe5b54c8c43d2dc35ae1f82d71ec073e7be032
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530662"
---
# <a name="connect-to-hardware"></a>ハードウェアへの接続します。


このトピックでは、センサー ドライバーが、割り当てられたハードウェア リソースを決定する方法を示していますし、ADXL345 ハードウェアに接続できるように、I2C ドライバー コント ローラーに接続します。

次のセクションでは、ハードウェアに接続するには、センサー ドライバーを作成する方法を表示するためのテスト ケースとして、ADXL345 加速度計から開発されたドライバーのサンプル コード スニペットを使用します。 既に同意していないに移動、 [ADXL345Acc サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/1fbea08887e10e087c3f6bb0be8968e29e20cc84/sensors/ADXL345Acc)github の説明と共に利用できるようにします。

これらのコード スニペットは、センサー ドライバー ファイルの重要なセクションの一部を強調表示します。 ドライバーのしくみを理解して、センサーのこれらのファイルをカスタマイズする方法を把握することができる、全体のすべてのドライバー ファイルを確認する必要があります。

## <a name="prepare-hardware-resources"></a>ハードウェア リソースを準備します。


1. をクリックして、 *device.cpp*ファイルを開くと、検索し、 **OnPrepareHardware**関数。 その関数内では、次のコードを検索します。
   ```cpp
   // Create WDFOBJECT for the sensor
    WDF_OBJECT_ATTRIBUTES sensorAttributes;
    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&sensorAttributes, ADXL345AccDevice);
   ```

上記のコードでは、センサー オブジェクトを作成し、適切なデバイス コンテキストを割り当てます。

2. 次のコードを検索します。
   ```cpp
   // Register sensor instance with clx
    SENSOROBJECT SensorInstance = NULL;
    NTSTATUS Status = SensorsCxSensorCreate(Device, &sensorAttributes, &SensorInstance);
   ```

上記のコードでは、センサー クラスの拡張機能をセンサーのインスタンスを登録します。 同じチップ内の複数のセンサーがあるシナリオのために、デバイスのインスタンスではなく、センサーのインスタンスが作成されます。

3. 次のコードを検索します。
   ```cpp
   // Initialize sensor instance with clx
    SENSOR_CONFIG SensorConfig;
    SENSOR_CONFIG_INIT(&SensorConfig);
    SensorConfig.pEnumerationList = pAccDevice->m_pEnumerationProperties;
    Status = SensorsCxSensorInitialize(SensorInstance, &SensorConfig);
   ```

上記のコードでは、センサーのインスタンスを初期化するのにセンサー クラスの拡張機能を使用します。

4. 次のコードを検索します。
   ```cpp
   Status = pAccDevice->ConfigureIoTarget(ResourcesRaw, ResourcesTranslated);
   ```

上記のコードは、センサー ドライバーの I/O ターゲット オブジェクトを構成します。 I/O のターゲット オブジェクトは、他のドライバーとの通信にセンサー ドライバーを使用できます。

## <a name="configure-the-device-with-default-settings"></a>既定の設定で、デバイスを構成します。


D0 は、デバイスのアクティブな状態であることに注意してください。 D0 にし、デバイス自体には、デバイスのレジスタでは、この構成の設定が必要ですし、I2C 経由でデバイスと通信します。 書き込みを実行する前にこのリソースのロックを保持するか、読み取る必要があります。

内で、 *device.cpp*ファイルで、検索、 **OnD0Entry**関数を呼び出していることに注意してください。 **PowerOn**、ADXL345 コンテキストを使用して、デバイスの電源を入れての作業を行います。 内で、 **PowerOn**関数を次のコードを検索します。
1.
```cpp
WdfWaitLockAcquire(m_I2CWaitLock, NULL);
```

上記のコードは、I2C バスのロックの取得に使用されます。

2. 次のコードを検索します。
   ```cpp
   // Write the default device configuration to the device
   For (DWORD i = 0; i < ARRAYSIZE(g_ConfigurationSettings); i++)
   {
       REGISTER_SETTING setting = g_ConfigurationSettings[i];
       Status = I2CSensorWriteRegister(m_I2CIoTarget, setting.Register, &setting.Value, sizeof(setting.Value));
       if (!NT_SUCCESS(Status))
       {
           TraceError("ACC %!FUNC! I2CSensorReadRegister from 0x%02x failed! %!STATUS!", setting.Register, Status);
           WdfWaitLockRelease(m_I2CWaitLock);
           return Status

       }
    }
   ```

For ループは、デバイスのレジスタに既定の構成設定を記述に使用されます。

3. 次のコードを検索します。
   ```cpp
   // Release the I2C bus lock
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);

   InitPropVariantFromUInt32(SensorState_Idle, &(m_pSensorProperties->List[SENSOR_PROPERTY_STATE].Value));
   m_PoweredOn = true;
   ```

デバイスが正常に構成した後、WdfWaitLockRelease は I2C バスのロックの解放に使用されます。

4. 閉じる、 *device.cpp*ファイル。
   ## <a name="start-the-device-activity"></a>デバイスのアクティビティを開始します。


5. をクリックして、 *client.cpp*を開き、ファイルを見つけて、 **OnStart**関数。
6. センサー デバイスのロックを取得するために使用する次のコードを確認します。
   ```cpp
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   ```

7. 次のコードを検索します。
   ```cpp
   // Set accelerometer to measurement mode
   REGISTER_SETTING RegisterSetting = { ADXL345_POWER_CTL, ADXL345_POWER_CTL_MEASURE };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

加速度計に設定する I2C 接続を使用する上記のコードで*測定モード*センサーの値を読み取るためすぐに使えるようにします。 参照してください、 *adxl345.h* ADXL345 の定義については、ヘッダー ファイル\_POWER\_CTL、ADXL345\_POWER\_CTL\_メジャーと、サンプルで使用されるその他のいくつかの定数センサー ドライバー。

4. 次のコードを検索します。
   ```cpp
   // Enable interrupts
   RegisterSetting = { ADXL345_INT_ENABLE, ADXL345_INT_ACTIVITY };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);
   ```

*RegisterSetting*パラメーター、センサーの割り込みを有効にします。 WdfWaitLockRelease を使用して、I2C バスのロックを解除します。

## <a name="stop-the-device-activity-and-set-device-to-standby"></a>デバイスのアクティビティとスタンバイ状態に一連のデバイスを停止します。


1. 内で、 *client.cpp*ファイルで、次のコードを検索、 **OnStop**関数。
   ```cpp
   // Disable interrupts
   REGISTER_SETTING RegisterSetting = { ADXL345_INT_ENABLE, 0 };
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

上記のコードでは、 *RegisterSetting*パラメーターはレジスタのアドレスと構成のコードをキャプチャします。 ここで RegisterSetting.Register は、RegisterSetting.Value は、デバイスからの割り込みの発行を停止するには、登録を構成する間、割り込みを有効にするレジスタのアドレスです。

2. 次のコードは、保留中ある可能性がありますを未処理の割り込みをクリアします。 デバイスから。
   ```cpp
   // Clear any stale interrupts
   RegisterSetting = { ADXL345_INT_SOURCE, 0 };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

3. 次のコードは、デバイスをスタンバイ モードに設定を検索します。 この設定は、デバイスのアクティビティを停止します。
   ```cpp
   // Set accelerometer to standby
   RegisterSetting = { ADXL345_POWER_CTL, ADXL345_POWER_CTL_STANDBY };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

## <a name="disconnect-hardware-resources"></a>ハードウェア リソースを切断します。


フレームワークを使用している、 **OnReleaseHardware**を停止するか、デバイスを削除する I/O 要求パケット (IRP) への応答内のハードウェア リソースを切断する関数。

1. 内で、 *client.cpp*ファイルに、 **DeInit**関数 (によって呼び出されます**OnReleaseHardware**で、 *device.cpp*ファイル) を検索します次のコード:
   ```cpp
   // Delete lock
   WdfObjectDelete(m_I2CWaitLock);
   m_I2CWaitLock = NULL;
   ```

上記のコードを使用して、デバイス オブジェクトの待機のロックを削除します。

2. センサーのインスタンスを削除するために使用する次のコードを検索します。
   ```cpp
   // Delete sensor instance
   WdfObjectDelete(m_SensorInstance);
   ```

3. 閉じる、 *client.cpp*ファイル。







