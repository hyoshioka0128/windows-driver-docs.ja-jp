---
title: ドライバーの初期化
description: ドライバーの初期化
ms.assetid: 9886BBBC-7EE5-45AF-AEDD-75C0885C622B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdde029776cb127adc8336d4d884b3ee454311dd
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264449"
---
# <a name="driver-initialization"></a>ドライバーの初期化


ドライバーの初期化は、ユーザーモードドライバーの機能のより複雑なフェーズの1つです。 これは、サンプルドライバーのコンポーネントのほとんど (すべてではない場合) に接しています。

### <a name="acpi-configuration-and-initialization"></a>ACPI の構成と初期化

| モジュール               | クラス/インターフェイス |
|----------------------|-----------------|
| SpbAccelerometer asl | なし             |

 

このサンプルドライバーは、センサーが I2C バスに永続的に接続するように設計されています。 プラグアンドプレイをサポートする代わりに、Advanced Configuration and Power Interface (ACPI) をサポートしています。

ACPI を使用すると、Windows はデバイスの構成と電源管理を制御できます。 ACPI 仕様には、Windows デバイスと、システムボードに接続されている周辺機器をリンクするテーブルの定義があります。 差別化システム説明表 (DSDT) は、システムに接続されている周辺機器 (センサーを含む) を示します。 これは、ACPI コンピューター言語 (AML) と呼ばれるバイナリ形式で格納されます。 DSDT テーブルの詳細については、「ACPI システムの説明表」を参照してください。 (一部のシステムでは、周辺機器を示すために "セカンダリシステムの説明" テーブル (SSDT) も使用されています)。

Windows SoC デバイスにセンサーデバイスとドライバーをインストールするには、対応するノードを使用して DSDT テーブルを更新する必要があります。 このノードには、サンプルデバイスのコントローラーとコネクタに関する情報が含まれています。 Windows とドライバーがノードのデータを使用する方法を次に示します。

1.  プラグアンドプレイ (PnP) マネージャーは、ACPI ドライバーからデバイス接続情報を取得します。
2.  PnP マネージャーは、バス接続を表す接続 ID を作成します。
3.  PnP マネージャーは、接続 ID をハードウェアリソースとしてサンプルドライバーに渡します。
4.  サンプルドライバーでは、接続 ID を使用してセンサーデバイスへの論理接続を開き、接続のハンドルを取得します。
5.  ドライバーは、このハンドルを、デバイスに送信する i/o 要求のターゲットとして指定します。

### <a name="updating-the-dsdt-table"></a>DSDT テーブルを更新しています

DSDT テーブルを更新する方法を説明する手順については、[サメ Cove のサンプルデバイスとドライバーのインストール](installing-the-sample-device-and-driver-on-your-sharks-cove-board.md)に関するトピックを参照してください。

### <a name="modifying-the-sample-asl-file"></a>サンプルの ASL ファイルの変更

別のデバイスをサポートするようにサンプルドライバーを変更する場合は、サンプルの ASL ファイルに対して対応する更新を行います。 ほとんどの更新は、 \_ デバイスに必要な I2C および GPIO リソースを指定するファイルの CRS セクションに対して行われます。 また、 \_ 更新された INF ファイル内の対応するエントリと一致する一意の HID エントリを指定する必要もあります。

### <a name="decoding-i2c-or-gpio-resources"></a>I2C リソースまたは GPIO リソースのデコード

/Resデコードオプションを指定しない場合、 \_ CRS セクションにバイナリ blob が含まれます。 このセクションを人間が判読できるテキストに変換するには、次に示すように、/Asl.exe を適用します。

### <a name="updating-the-windows-setup-information-file"></a>Windows セットアップ情報ファイルを更新しています

| モジュール               | クラス/インターフェイス |
|----------------------|-----------------|
| SpbAccelerometer | なし             |

 

DSDT テーブルを更新するだけでなく、Windows セットアップ情報ファイル (INF) を更新して、デバイスで ACPI がサポートされるように指定する必要があります。 センサーは常に ACPI によって列挙されるため、INF ファイル内のハードウェア識別子には "ACPI" 文字列が含まれている必要があります。

```cpp
; =================== Manufacturer/Models sections =======================

[Manufacturer]
%MSFT%                      = Microsoft,NTx86

[Microsoft.NTx86]
%SpbAccelerometer.DeviceDesc% = SpbAccelerometer_Install,ACPI\SpbAccelerometer
```

### <a name="initializing-the-driver-and-device"></a>ドライバーとデバイスを初期化しています

| モジュール      | クラス/インターフェイス |
|-------------|-----------------|
| DllMain | なし             |
| デバイス .cpp  | CMyDevice       |
| ドライバー .cpp  | CMyDriver       |
| キュー .cpp   | CMyQueue        |

 

次のメソッドは、初期初期化フェーズ中に Windows またはドライバーによって呼び出されます。 デバイスの事前初期化方法は、ドライバーでサポートされているすべてのデバイスに適用されます。 これらは、モジュールの .cpp に表示されます。

|  手順   | メソッド                        | 呼び出し元                                                         | 目的                                                                                                       |
|-----|-------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 1   | **DllGetClassObject**         | WUDFHost.exe                                                       | ドライバーのクラスオブジェクトを取得します。 (すべての COM DLL に必要です)。                                                   |
| 2   | **CMyDevice:: OnQueryRemove**  | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 |                                                                                                               |
| 3   | **CMyDriver:: OnDeviceAdd**    | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | デバイスが追加されたことをドライバーに通知します。                                                             |
| 4   | **CMyDevice:: Configure**      | **CMyDriver:: OnDeviceAdd**                                         | デバイスのキューおよび対応するコールバックオブジェクトを構成します。                                        |
| 5   | **CMyQueue: CreateInstance**   | **CMyDevice:: Configure**                                           | デバイスのキューコールバックのインスタンスを作成します。                                                            |
| 6   | **CMyDevice:: CreateInstance** | **CMyDevice:: OnDeviceAdd**                                         | 特定のデバイス (この場合は加速度計) に対応するデバイスオブジェクトのインスタンスを作成します。 |
| 7   | **CMyDevice:: Initialize**     | **CMyDevice:: CreateInstance**                                      | デバイスコールバックオブジェクトを初期化します。                                                                       |

 

### <a name="establishing-a-data-connection"></a>データ接続の確立

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| デバイス .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice | CAccelerometerDevice |

 

次のメソッドは、初期化時にドライバーによって呼び出され、デバイスオブジェクトを準備し、ACPI 構成データを取得して、データ接続の割り込みを作成します。 サンプルドライバーでは、これらのメソッドは AccelerometerDevice ファイルにあります。

コンパスなどの別のデバイスをサポートするようにサンプルドライバーを移植している場合は、parallel モジュールを作成します。 CAccelerometerDevice クラスを CCompassDevice クラスに置き換え、デバイスのオブジェクト、データ、および割り込みをサポートするように、サンプルのモジュール内のメソッドを修正します。

| 手順    | メソッド                                                 | 呼び出し元                                                         | 目的                                                                                                                |
|-----|--------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice:: On Hardware**                       | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | ドライバーが特定のデバイスにアクセスできるようにするために必要な操作を開始します。                                       |
| 2   | **CSensorDdi:: Initialize**                             | **CMyDevice:: On Hardware**                                   | センサーデバイスオブジェクトを作成し、初期化します。                                                                        |
| 3   | **CSensorDevice:: Initialize**                          | **CSensorDdi:: Initialize**                                         | センサードライバーインターフェイス、クライアントマネージャー、およびレポートマネージャーを初期化します。                                   |
| 4   | **CAccelerometerDevice:: InitializeDevice**             | **CSensorDevice:: Initialize**                                      | 加速度計 device オブジェクトを初期化します。                                                                           |
| 5   | **CAccelerometerDevice::GetConfigurationData**         | **CAccelerometerDevice:: InitializeDevice**                         | ACPI からの構成データの取得を開始します。                                                               |
| 6   | **CAccelerometerDevice::P repareInputParametersForDsm** | **CAccelerometerDevice::GetConfigurationData**                     | \_ \_ \_ デバイス固有のメソッド (DSM) 関数を呼び出す前に、acpi 入力バッファー (acpi EVAL 入力バッファー) を準備します。 |
| 7   | **CAccelerometerDevice::P arseAcpiOutputBuffer**        | **CAccelerometerDevice::GetConfigurationData**                     | ACPI 出力バッファー (ACPI \_ EVAL output buffer) で返された構成データを解析し \_ \_ ます。                |
| 8   | **CAccelerometerDevice::P arseResources**               | **CAccelerometerDevice:: InitializeDevice**                         | デバイスリソースを解析して、シリアル I2C 接続をサポートしていることを確認します。                                        |
| 9   | **CAccelerometerDevice:: ConnectInterrupt**             | **CAccelerometerDevice::P arseResources**                           | データ接続の割り込みを作成します。                                                                                 |

 

### <a name="initializing-the-spb-request-object"></a>SPB 要求オブジェクトを初期化しています

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| デバイス .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice | CAccelerometerDevice |
| SpbRequest. .cpp          | CSpbRequest          |

 

次のメソッドは、初期化中にドライバーによって呼び出され、基になる SPB コントローラーへのファイルハンドルを開きます。 (このシーケンスの最初の4つのメソッドは、データ接続シーケンスの最初の4つのメソッドと同じであることに注意してください)。

| 手順   | メソッド                                      | 呼び出し元                                                         | 目的                                                                                                                                          |
|-----|---------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice:: On Hardware**            | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | ドライバーが特定のデバイスにアクセスできるようにするために必要な操作を開始します。                                                                |
| 2   | **CSensorDdi:: Initialize**                  | **CMyDevice:: On Hardware**                                   | センサーデバイスオブジェクトを作成し、初期化します。                                                                                                |
| 3   | **CSensorDevice:: Initialize**               | **CSensorDdi:: Initialize**                                         | センサードライバーインターフェイス、クライアントマネージャー、およびレポートマネージャーを初期化します。                                                             |
| 4   | **CAccelerometerDevice:: InitializeDevice**  | **CSensorDevice:: Initialize**                                      | 加速度計 device オブジェクトを初期化します。                                                                                                     |
| 5   | **CAccelerometerDevice::InitializeRequest** | **CAccelerometerDevice:: InitializeDevice**                         | SPB 要求オブジェクトの初期化プロセスを開始します (リソースハブのパスと、ドライバーが以前に取得した接続 ID を使用します)。 |
| 6   | **CSpbRequest:: Initialize**                 | **CAccelerometerDevice::InitializeRequest**                        | 基になる SPB へのファイルハンドルを開きます。                                                                                                        |

 

### <a name="initializing-the-supported-sensor-properties-and-data-fields"></a>サポートされているセンサーのプロパティとデータフィールドを初期化しています

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| デバイス .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice | CAccelerometerDevice |
| SpbRequest. .cpp          | CSpbRequest          |

 

次のメソッドは、初期化時にドライバーによって呼び出され、センサーによってサポートされるプロパティとデータフィールドを取得します。 Windows センサープラットフォームの場合、加速度計プロパティは、センサーのレポート間隔やサポートされる最小レポート間隔など、読み取りまたは読み取り/書き込みのデータに対応します。 データフィールドは、X、Y、Z 軸に沿った実際の加速度計の読み取りに対応しています。 (このシーケンスの最初の3つのメソッドは、前のデータ接続の最初の3つのメソッドと、SPB の要求オブジェクトのシーケンスと同じであることに注意してください)。

| 手順  | メソッド                                             | 呼び出し元                                                         | 目的                                                                                                               |
|-----|----------------------------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice:: On Hardware**                   | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | ドライバーが特定のデバイスにアクセスできるようにするために必要な操作を開始します。                                     |
| 2   | **CSensorDdi:: Initialize**                         | **CMyDevice:: On Hardware**                                   | センサーデバイスオブジェクトを作成して初期化します。                                                                      |
| 3   | **CSensorDevice:: Initialize**                      | **CSensorDdi:: Initialize**                                         | センサードライバーインターフェイス、クライアントマネージャー、およびレポートマネージャーを初期化します。                                  |
| 4   | **CSensorDevice:: InitializeSensorDriverInterface** | **CSensorDevice:: Initialize**                                      | プロパティキーと datafield 値を格納する**Iportabledevicevalues**オブジェクトの初期化を開始します。 |
| 5   | **CSensorDevice:: AddPropertyKeys**                 | **CSensorDevice:: InitializeSensorDriverInterface**                 | サポートされているプロパティを反復処理し、それぞれの**Propertykey**を追加します。                                        |
| 6   | **CAccelerometerDevice:: GetSupportedProperties**   | **CSensorDevice:: AddPropertyKeys**                                 | 指定されたデバイスのプロパティの**Propertykey**構造体を取得します。                                                |
| 7   | **CSensorDevice:: AddDataFieldKeys**                | **CSensorDevice:: InitializeSensorDriverInterface**                 | サポートされているデータフィールドを反復処理し、それぞれに**Propertykey**を追加します。                                       |
| 8   | **CSensorDevice:: GetSupportedDataFields**          | **CSensorDevice:: AddDataFieldKeys**                                | 指定されたデバイスのデータフィールドの**Propertykey**を取得します。                                                         |

 

### <a name="initializing-the-persistent-unique-id-property"></a>永続的な一意の ID プロパティを初期化しています

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| デバイス .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

次のメソッドは、初期化時にドライバーによって呼び出され、センサーの永続的な一意識別子 (PUID) を初期化します。 Windows では、 **PUID**を使用して、デバイスセッション間でデータを保持します。 (このシーケンスの最初の4つのメソッドは、前のプロパティとデータフィールドのシーケンスの最初の4つのメソッドと同じであることに注意してください)。

| 手順  | メソッド                                             | 呼び出し元                                                         | 目的                                                                                                   |
|-----|----------------------------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice:: On Hardware**                   | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | ドライバーが特定のデバイスにアクセスできるようにするために必要な操作を開始します。                         |
| 2   | **CSensorDdi:: Initialize**                         | **CMyDevice:: On Hardware**                                   | センサーデバイスオブジェクトを作成して初期化します。                                                          |
| 3   | **CSensorDevice:: Initialize**                      | **CSensorDdi:: Initialize**                                         | センサードライバーインターフェイス、クライアントマネージャー、およびレポートマネージャーを初期化します。                      |
| 4   | **CSensorDevice:: InitializeSensorDriverInterface** | **CSensorDevice:: Initialize**                                      | プロパティキーと datafield 値を格納するオブジェクトの初期化を開始します。               |
| 5   | **CSensorDevice:: SetUniqueID**                     | **CSensorDevice:: InitializeSensorDriverInterface**                 | ドライバーがセッション間で使用できる永続的な一意識別子 (PUID) を取得するメソッドを呼び出します。 |
| 6   | **CAcclerometerDevice:: GetSensorObjectID**         | **CSensorDevice:: SetUniqueID**                                     | 加速度計の永続的な識別子 ("ADXL345") を取得します。                                               |

 

### <a name="setting-the-default-property-values"></a>既定のプロパティ値の設定

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| デバイス .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

Windows センサープラットフォームでは、センサーの種類、製造元の名前、センサーモデル、およびシリアル番号の既定のプロパティ値がサポートされています。 SpbAccelerometer サンプルのコードでは、ドライバーとデバイスの初期化フェーズの一部としてこれらのプロパティを設定します。 次のメソッドは、初期化中に、加速度計の既定値を設定するために、ドライバーによって呼び出されます。 (このシーケンスの最初の4つのメソッドは、前のプロパティ設定シーケンスの最初の4つのメソッドと同じであることに注意してください)。

| 手順   | メソッド                                             | 呼び出し元                                                         | 目的                                                                                           |
|-----|----------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice:: On Hardware**                   | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | ドライバーが特定のデバイスにアクセスできるようにするために必要な操作を開始します。                 |
| 2   | **CSensorDdi:: Initialize**                         | **CMyDevice:: On Hardware**                                   | センサーデバイスオブジェクトを作成し、初期化します。                                                   |
| 3   | **CSensorDevice:: Initialize**                      | **CSensorDdi:: Initialize**                                         | センサードライバーインターフェイス、クライアントマネージャー、およびレポートマネージャーを初期化します。              |
| 4   | **CSensorDevice:: InitializeSensorDriverInterface** | **CSensorDevice:: Initialize**                                      | プロパティキーと datafield 値を格納するオブジェクトの初期化を開始します。       |
| 5   | **CAccelerometerDevice:: SetDefaultPropertyValues** | **CSensorDevice:: InitializeSensorDriverInterface**                 | 加速度計 (製造元、モデル、シリアル番号など) の既定のプロパティ値を設定します。 |

 

### <a name="retrieving-the-default-writeable-properties"></a>既定の書き込み可能プロパティの取得

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| デバイス .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

Windows センサープラットフォームでは、センサーの読み取り専用プロパティと読み取り/書き込みプロパティがサポートされています。これは、既定のプロパティにも当てはまります。 SpbAccelerometer サンプルのコードは、ドライバーとデバイスの初期化フェーズの一部として、書き込み可能な (または設定可能な) 既定のプロパティの一覧を取得します。 次のメソッドは、初期化中に、加速度計のこれらのプロパティを取得するために、ドライバーによって呼び出されます。 (このシーケンスの最初の4つのメソッドは、前のプロパティ設定シーケンスの最初の4つのメソッドと同じであることに注意してください)。

| 手順   | メソッド                                             | 呼び出し元                                                         | 目的                                                                                           |
|-----|----------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice:: On Hardware**                   | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | ドライバーが特定のデバイスにアクセスできるようにするために必要な操作を開始します。                  |
| 2   | **CSensorDdi:: Initialize**                         | **CMyDevice:: On Hardware**                                   | センサーデバイスオブジェクトを作成して初期化します。                                                  |
| 3   | **CSensorDevice:: Initialize**                      | **CSensorDdi:: Initialize**                                         | センサードライバーインターフェイス、クライアントマネージャー、およびレポートマネージャーを初期化します。              |
| 4   | **CSensorDevice:: InitializeSensorDriverInterface** | **CSensorDevice:: Initialize**                                      | プロパティキーと datafield 値を格納するオブジェクトの初期化を開始します。       |
| 5   | **CAccelerometerDevice:: SetDefaultPropertyValues** | **CSensorDevice:: InitializeSensorDriverInterface**                 | 加速度計 (製造元、モデル、シリアル番号など) の既定のプロパティ値を設定します。 |

 

### <a name="activating-support-for-events"></a>イベントのサポートのアクティブ化

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| デバイス .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

Windows センサープラットフォームでは、イベントがサポートされています。 アプリケーションは、ドライバーから通知を取得するためにイベントハンドラーを登録します。 加速度計の場合、特定の変更の感度 (G force で測定) が経過するか、現在のレポートの期間が経過すると、これらの通知がトリガーされます。

センサープラットフォームでイベントモデルをサポートするには、ドライバーがスレッドをアクティブにしてイベント通知を処理する必要があります。 次のメソッドは、このアクティブ化を実行するために、初期化中にドライバーによって呼び出されます。 (このシーケンスの最初の3つのメソッドは、前のシーケンスの数値の最初の3つのメソッドと同じであることに注意してください)。

| 手順   | メソッド                                         | 呼び出し元                                                         | 目的                                                                              |
|-----|------------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 1   | **CMyDevice:: On Hardware**               | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | ドライバーが特定のデバイスにアクセスできるようにするために必要な操作を開始します。    |
| 2   | **CSensorDdi:: Initialize**                     | **CMyDevice:: On Hardware**                                   | センサーデバイスオブジェクトを作成し、初期化します。                                    |
| 3   | **CSensorDevice:: Initialize**                  | **CSensorDdi:: Initialize**                                         | センサードライバーインターフェイス、クライアントマネージャー、およびレポートマネージャーを初期化します。 |
| 4   | **CReportManager:: Initialize**                 | **CSensorDevice:: Initialize**                                      | イベントを処理するために使用するスレッドを作成します。                                            |
| 5   | **CReportManager:: アクティブ Dataeventingthread** | **CReportManager:: Initialize**                                     | 前のメソッドによって作成されたスレッドをアクティブにします。                                 |

 

### <a name="initializing-the-class-extension"></a>クラス拡張の初期化

| モジュール     | クラス/インターフェイス |
|------------|-----------------|
| デバイス .cpp | CMyDevice       |

 

Windows センサープラットフォームにはセンサー API のクラス拡張機能があり、センサーデータを取得してイベント通知を発生させるための標準的なメカニズムを提供します。 このサンプルドライバーは、 **ISensorClassExtension:: Initialize**メソッドを呼び出して、 **CMyDevice:: on hardware**の呼び出しを受け取った後に、クラス拡張を初期化します。

### <a name="configuring-the-device-and-placing-it-in-standby-mode"></a>デバイスを構成してスタンバイモードにする

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| デバイス .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

デバイスとドライバーの初期化の最後のシーケンスでは、ADXL345 を構成し、スタンバイモードにします。 (この一連の書き込み操作と読み取り操作は、デバイスが構成されるまで複数回繰り返されます)。

| 手順  | メソッド                                          | 呼び出し元                                                         | 目的                                                                               |
|-----|-------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnD0Entry**                        | WUDFx.dll (Windows ユーザーモードドライバーフレームワークのコンポーネント)。 | 新しいデバイスがシステムに表示されたときに呼び出されます。                                      |
| 2   | **CSensorDdi:: Start**                           | **CMyDevice::OnD0Entry**                                           | CSensorDevice:: Start を呼び出すパススルーメソッド。                                |
| 3   | **CSensorDevice:: Start**                        | **CSensorDdi:: Start**                                              | デバイス構成プロセスを開始します。                                           |
| 4   | **CAccelerometerDevice::ConfigureHardware**     | **CSensorDevice:: Start**                                           | ADXL345 の指定したレジスタに値を書き込む操作を開始します。 |
| 5   | **CAcclerometerDevice::WriteRegister**          | **CAccelerometerDevice::ConfigureHardware**                        | ADXL345 の指定したレジスタに値を書き込む操作を開始します。 |
| 6   | **CSpbRequest:: CreateAndSendWrite**             | **CAcclerometerDevice::WriteRegister**                             | I2C バス経由で書き込み要求を送信します。                                          |
| 7   | **CAcclerometerDevice:: ReadRegister**           | **CAccelerometerDevice::ConfigureHardware**                        | 指定された ADXL345 register から値を読み取る操作を開始します。       |
| 8   | **CSpbRequest:: CreateAndSendWriteReadSequence** | **CAcclerometerDevice:: ReadRegister**                              | は、I2C バス経由で読み取り結果を受信します。                                           |
| 9   | **CSpbRequest:: CreateAndSendIoctl**             | **CSpbRequest:: CreateAndSendWriteReadSequence**                    | IOCTL 要求を作成して送信するヘルパーメソッド。                                |

 

ほとんどのデバイス構成作業は、一連の**CAccelerometerDevice:: WriteRegister**メソッドと**CAccelerometerDevice:: readregister**メソッド呼び出しによって行われます。 ドライバーは、::**WriteRegister**メソッドを使用して、いずれかの ADXL345 レジスタに値を書き込みます。次に、対応する::**Readregister**メソッドで返された値を調べて、書き込み操作が成功したことを確認します。 書き込み操作と読み取り操作の完全なシーケンスを次に示します。

| 手順 | Method                                  | [登録] | Data                | 目的                                                                                                            |
|-----|-----------------------------------------|----------|---------------------|--------------------------------------------------------------------------------------------------------------------|
| 1   | **CAccelerometerDevice::WriteRegister** | **0x2d** | **' \\ 0 ' (0x00)**    | センサーの電源管理登録をリセットし、デバイスをスタンバイモードにします。                                   |
| 2   | **CAccelerometerDevice:: ReadRegister**  | **0x2d** | **' \\ 0 ' (0x00)**    | 返されるレジスタ値は、書き込み操作が成功したことを示します。                                          |
| 3   | **CAccelerometerDevice::WriteRegister** | **0x31** | **' \\ v ' (0x0b)**    | デバイスを、+/-16G の各軸に沿った範囲で、完全解像度モードに設定します。                                   |
| 4   | **CAccelerometerDevice:: ReadRegister**  | **0x31** | **' \\ v ' (0x0b**     | 返されるレジスタ値は、書き込み操作が成功したことを示します。                                          |
| 5   | **CAccelerometerDevice::WriteRegister** | **0x38** | **' \\ 0 ' (0x00)**    | センサーの FIFO 制御レジスタをバイパスモードにリセットします。                                                      |
| 6   | **CAccelerometerDevice:: ReadRegister**  | **0x38** | **' \\ 0 ' (0x00)**    | 返されるレジスタ値は、書き込み操作が成功したことを示します。                                          |
| 7   | **CAccelerometerDevice::WriteRegister** | **0x2C** | **' \\ a ' (0x07)**    | BW \_ RATE 登録を低電力モードで開始するように設定します。                                                             |
| 8   | **CAccelerometerDevice:: ReadRegister**  | **0x2C** | **' \\ a ' (0x07)**    | 返されるレジスタ値は、書き込み操作が成功したことを示します。                                          |
| 9   | **CAccelerometerDevice::WriteRegister** | **0x24** | **' \\ x1 ' (0x01)**   | TRESH \_ ACT (アクティビティしきい値) レジスタを1に設定します。                                                            |
| 10  | **CAccelerometerDevice:: ReadRegister**  | **0x24** | **' \\ x1 ' (0x01)**   |                                                                                                                    |
| 11  | **CAccelerometerDevice::WriteRegister** | **0x27** | **0xf0 です**          | ACT \_ inact \_ CTL (アクティブ/非アクティブ) レジスタを0xf0 に設定します。                                                       |
| 12  | **CAccelerometerDevice:: ReadRegister**  | **0x27** | **0xf0 です**          | 返されるレジスタ値は、書き込み操作が成功したことを示します。                                              |
| 13  | **CAccelerometerDevice::WriteRegister** | **0x2f** | **' \\ 0x10 ' (0x10)** | INT \_ マップ (割り込みマッピング) レジスタを設定します。 値が0x10 の場合は、ウォーターマークが INT2 pin にマップされることを要求します。 |
| 14  | **CAccelerometerDevice:: ReadRegister**  | **0x2f** | **' \\ 0x10 ' (0x10)** | 返されるレジスタ値は、書き込み操作が成功したことを示します。                                          |


ドライバーとデバイスの構成が完了すると、初期化シーケンスが完了し、アプリがセンサーデータの受信を開始できるようになります。

 

 




