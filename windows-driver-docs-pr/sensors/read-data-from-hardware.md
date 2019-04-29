---
title: ハードウェアからデータを読み取る
description: このトピックでは、サンプル センサー ドライバーが読み取り要求に応答センサー ハードウェア (加速度計) からデータを読み取る方法を示します。
ms.assetid: 4C01324D-3C4D-4028-A7DE-0AD8F2233071
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01470a45d3bf3760020a9cd8f8edd1cf8ed13586
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330058"
---
# <a name="read-data-from-hardware"></a>ハードウェアからデータを読み取る


このトピックでは、サンプル センサー ドライバーが読み取り要求に応答センサー ハードウェア (加速度計) からデータを読み取る方法を示します。

通常、センサー ドライバーの"最上位の end"はデータを読み取る、センサーに接続できるアプリケーションにアクセスできるように設計されています。 サンプル センサー ドライバーは、加速度計からサンプル データを読み取るための関数の読み取りデータに直接ドライバーの"最上位の end"が関連付けられます。 次のセクションでは、データの読み取りがセンサー ドライバーのサンプルで実装する方法について説明します。

## <a name="handle-read-requests"></a>ハンドルが読み取り要求


1. をクリックして、 *client.cpp*を開き、ファイルを見つけて、 **OnInterruptIsr**関数。
2. 次のコードを検索します。

```cpp
// Read the Interrupt source
   BYTE IntSrcBuffer = 0;
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   Status = I2CSensorReadRegister(pAccDevice->m_I2CIoTarget, ADXL345_INT_SOURCE, &IntSrcBuffer, sizeof(IntSrcBuffer));
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);
```

上記のコードが最初に、デバイスのロックを取得し、割り込みのソースを決定しを使用して、 **I2CSensorReadRegister**関数。 コードは、最後に、デバイスのロックを解放します。

3. 次のコードを検索します。

```cpp
// Create work item
   InterruptRecognized = TRUE;

   BOOLEAN WorkItemQueued = WdfInterruptQueueWorkItemForIsr(Interrupt);
   TraceVerbose("%!FUNC! Work item %s queued for interrupt", WorkItemQueued ? "" : " already");
```

センサー ドライバーを使用して、センサー ドライバーでは、割り込みのソースが正常に判断、 **WdfInterruptQueueWorkItemForIsr** framework 用のキューに置かれた作業項目を作成します。

## <a name="read-sensor-data"></a>センサー データを読み取る


センサー ドライバーのサンプルを使用して**GetData**センサー インスタンスを取得する、デバイスのロックを取得し、センサー データを読み取る。 ときに、 **GetData**関数呼び出しが返されます、ロックを解放します。

1. 内で、 *client.cpp*ファイルで、検索、 **OnInterruptWorkItem**関数。 その関数内では、次のコードを確認します。

```cpp
// Invoke the function that Reads the device data
   WdfInterruptAcquireLock(Interrupt);
   Status = pAccDevice->GetData();
   WdfInterruptReleaseLock(Interrupt);
```

2. 検索、 **GetData**関数、および次のコードを検索します。
   ```cpp
   // Read the device data
   BYTE DataBuffer[ADXL345_DATA_REPORT_SIZE_BYTES];
   WdfWaitLockAcquire(m_I2CWaitLock, NULL);
   Status = I2CSensorReadRegister(m_I2CIoTarget, ADXL345_DATA_X0, &DataBuffer[0], sizeof(DataBuffer));
   WdfWaitLockRelease(m_I2CWaitLock);
   ```

上記のコードがサイズのバッファーを確保*DataBuffer*、I2C 接続を介してそのバッファーにデバイス データを読み込みます。

3. 次のコードを検索します。
   ```cpp
   // Add timestamp
   FILETIME Timestamp = {};
   GetSystemTimeAsFileTime(&Timestamp);
   InitPropVariantFromFileTime(&Timestamp, &(m_pSensorData->List[SENSOR_DATA_TIMESTAMP].Value));

   SensorsCxSensorDataReady(m_SensorInstance, m_pSensorData);
   ```

上記のコード、デバイスのデータにタイムスタンプを追加します。 デバイス コンテキスト内の場所にデータを保存しを使用して*m\_pSensorData*をポイントします。 これにより、使用可能なデータは、クラスの拡張機能に、スタックをさらにします。

4. 閉じる、 *client.cpp*ファイル。
 

 




