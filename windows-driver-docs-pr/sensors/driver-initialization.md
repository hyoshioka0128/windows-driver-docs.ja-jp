---
title: ドライバーの初期化
description: ドライバーの初期化
ms.assetid: 9886BBBC-7EE5-45AF-AEDD-75C0885C622B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecc49488e52a51cc37dd658c71740a486534a5b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377788"
---
# <a name="driver-initialization"></a>ドライバーの初期化


ドライバーの初期化では、ユーザー モード ドライバーの機能のより複雑な段階の 1 つです。 ドライバーのサンプルでは、コンポーネントの最も、全部ではありませんが接触します。

### <a name="acpi-configuration-and-initialization"></a>ACPI の構成と初期化

| モジュール               | クラス/インターフェイス |
|----------------------|-----------------|
| SpbAccelerometer.asl | なし             |

 

ドライバーのサンプルでは、センサーが完全に I2C バスに接続されているように設計されています。 プラグ アンド プレイをサポートしているのではなく、Advanced Configuration and Power Interface (ACPI) をサポートします。

ACPI は、Windows デバイスの構成と電源管理を制御できます。 ACPI の仕様には、テーブルの定義の Windows デバイスと周辺機器は、システム ボードに接続されているそのリンクがあります。 システムの説明の差別化されたテーブル (あります)、システムに接続されている周辺機器の説明、センサーなど。 ACPI 機械語 (AML) としての既知のバイナリ形式で格納されます。 します。 テーブルの詳細については、ACPI システム説明テーブルのトピックを参照してください。 (一部のシステムが、周辺機器を記述する、セカンダリ システムの説明テーブル (SSDT) をも使用することに注意してください)。

SoC の Windows デバイス、センサー デバイスとドライバーをインストールするには、対応するノードでします。 テーブルを更新する必要があります。 このノードでは、サンプル デバイスのコント ローラーとコネクタに関する情報があります。 Windows とドライバーの使い方、データ ノードで次に示します。

1.  1. プラグ アンド プレイ (PnP) マネージャーでは、ACPI ドライバーからデバイスの接続情報を取得します。
2.  PnP マネージャーは、bus 接続を表す接続 ID を作成します。
3.  PnP マネージャーでは、ハードウェア リソースとしてサンプル ドライバーに接続 ID を渡します。
4.  ドライバーのサンプルでは、接続 ID を使用して、センサー デバイスへの論理接続を開くし、接続ハンドルを取得します。
5.  ドライバーは、I/O の対象の要求がデバイスに送信されますこのハンドルを指定します。

### <a name="updating-the-dsdt-table"></a>します。 テーブルの更新

します。 テーブルを更新する方法を説明する手順については、を参照してください、[サンプル デバイスとドライバーをインストール、サメ Cove](installing-the-sample-device-and-driver-on-your-sharks-cove-board.md)トピック。

### <a name="modifying-the-sample-asl-file"></a>サンプルの ASL ファイルを変更します。

別のデバイスをサポートするために、サンプル ドライバーを変更する場合は、サンプルの ASL ファイルに対応する更新プログラムが行います。 更新プログラムのほとんどがなります、 \_I2C を指定したファイルと、デバイスが必要な GPIO リソースの CRS セクション。 一意の提供する必要も\_HID エントリ、更新された INF ファイルに対応するエントリと一致します。

### <a name="decoding-i2c-or-gpio-resources"></a>GPIO、I2C、またはリソースのデコード

/Resdecode オプションを指定しない場合、 \_CRS セクションには、バイナリの blob にが含まれます。 このセクションを人間が判読できるテキストに変換するには、次のように/resdecode が適用されます。Asl.exe /tab:dsdt /resdecode

### <a name="updating-the-windows-setup-information-file"></a>Windows のセットアップ情報ファイルの更新

| モジュール               | クラス/インターフェイス |
|----------------------|-----------------|
| SpbAccelerometer.inf | なし             |

 

だけでなく、します。 テーブルを更新するには、Windows セットアップ情報ファイル、デバイスが ACPI をサポートしていることを指定するには、(INF) を更新する必要があります。 センサーは常に、ACPI で列挙、ために、INF ファイル内のハードウェア識別子は"ACPI"文字列を含める必要があります。

```cpp
; =================== Manufacturer/Models sections =======================

[Manufacturer]
%MSFT%                      = Microsoft,NTx86

[Microsoft.NTx86]
%SpbAccelerometer.DeviceDesc% = SpbAccelerometer_Install,ACPI\SpbAccelerometer
```

### <a name="initializing-the-driver-and-device"></a>ドライバーとデバイスの初期化

| モジュール      | クラス/インターフェイス |
|-------------|-----------------|
| DllMain.cpp | なし             |
| Device.cpp  | CMyDevice       |
| Driver.cpp  | CMyDriver       |
| Queue.cpp   | CMyQueue        |

 

以下の方法は、早期の初期化フェーズ中にドライバーまたは Windows によって呼び出されます。 デバイスの事前初期化メソッドは、ドライバーでサポートされる任意のデバイスに適用されます。 Device.cpp モジュールに表示されます。

|     | メソッド                        | によって呼び出されます                                                         | 目的                                                                                                       |
|-----|-------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 1   | **DllGetClassObject**         | WUDFHost.exe                                                       | ドライバーのクラスのオブジェクトを取得します。 (COM DLL に必要)。                                                   |
| 2   | **CMyDevice::OnQueryRemove**  | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 |                                                                                                               |
| 3   | **CMyDriver::OnDeviceAdd**    | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | デバイスが追加されたことをドライバーに通知します。                                                             |
| 4   | **CMyDevice::Configure**      | **CMyDriver::OnDeviceAdd**                                         | デバイスのキューおよび対応するコールバック オブジェクトを構成します。                                        |
| 5   | **CMyQueue:CreateInstance**   | **CMyDevice::Configure**                                           | デバイスのキューのコールバックのインスタンスを作成します                                                            |
| 6   | **CMyDevice::CreateInstance** | **CMyDevice::OnDeviceAdd**                                         | (この例では、加速度計) で特定のデバイスに対応するデバイス オブジェクトのインスタンスを作成します。 |
| 7   | **CMyDevice::Initialize**     | **CMyDevice::CreateInstance**                                      | デバイスのコールバック オブジェクトを初期化します。                                                                       |

 

### <a name="establishing-a-data-connection"></a>データ接続を確立します。

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

以下の方法は、デバイス オブジェクトを準備する、ACPI の構成データを取得し、データ接続の割り込みを作成するために初期化中に、ドライバーによって呼び出されます。 サンプル ドライバーの場合は、これらのメソッドを AccelerometerDevice.cpp ファイルにあります。

コンパスなどの別のデバイスをサポートするドライバーのサンプルを移植する場合は、並列のモジュール、CompassDevice.cpp を作成します。 CCompassDevice クラスを使用して、CAccelerometerDevice クラスを交換し、デバイスのオブジェクト、データ、および割り込みをサポートするために、サンプルのモジュール内のメソッドを変更します。

|     | メソッド                                                 | によって呼び出されます                                                         | 目的                                                                                                                |
|-----|--------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                       | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | ドライバーによって特定のデバイスがアクセスできるようにするために必要な操作を開始します。                                       |
| 2   | **CSensorDdi::Initialize**                             | **CMyDevice::OnPrepareHardware**                                   | 作成し、センサー デバイス オブジェクトを初期化します。                                                                        |
| 3   | **CSensorDevice::Initialize**                          | **CSensorDdi::Initialize**                                         | センサー ドライバー インターフェイス、クライアント マネージャー、およびレポート マネージャーを初期化します。                                   |
| 4   | **CAccelerometerDevice::InitializeDevice**             | **CSensorDevice::Initialize**                                      | 加速度計のデバイス オブジェクトを初期化します。                                                                           |
| 5   | **CAccelerometerDevice::GetConfigurationData**         | **CAccelerometerDevice::InitializeDevice**                         | ACPI から構成データの取得を開始します。                                                               |
| 6   | **CAccelerometerDevice::PrepareInputParametersForDsm** | **CAccelerometerDevice::GetConfigurationData**                     | ACPI の入力バッファーを確保します (ACPI\_EVAL\_入力\_バッファー) デバイス固有メソッド (DSM) 関数を呼び出す前にします。 |
| 7   | **CAccelerometerDevice::ParseAcpiOutputBuffer**        | **CAccelerometerDevice::GetConfigurationData**                     | ACPI の出力バッファーに返された構成データの解析 (ACPI\_EVAL\_出力\_バッファー)。                |
| 8   | **CAccelerometerDevice::ParseResources**               | **CAccelerometerDevice::InitializeDevice**                         | I2C のシリアル接続をサポートすることを確認し、デバイス リソースを解析します。                                        |
| 9   | **CAccelerometerDevice::ConnectInterrupt**             | **CAccelerometerDevice::ParseResources**                           | データ接続の割り込みを作成します。                                                                                 |

 

### <a name="initializing-the-spb-request-object"></a>SPB 要求オブジェクトの初期化

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SpbRequest.cpp          | CSpbRequest          |

 

以下の方法は、基になる SPB コント ローラーにファイル ハンドルを開くための初期化中に、ドライバーによって呼び出されます。 (このシーケンスの最初の 4 つのメソッドは、データ接続シーケンスの最初の 4 つのメソッドと同じことに注意してください)。

|     | メソッド                                      | によって呼び出されます                                                         | 目的                                                                                                                                          |
|-----|---------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**            | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | 特定のデバイスがアクセスできるようにするドライバーが必要な操作を開始します。                                                                |
| 2   | **CSensorDdi::Initialize**                  | **CMyDevice::OnPrepareHardware**                                   | 作成して、センサー デバイス オブジェクトを初期化します。                                                                                                |
| 3   | **CSensorDevice::Initialize**               | **CSensorDdi::Initialize**                                         | センサー ドライバー インターフェイス、クライアント マネージャー、およびレポート マネージャーを初期化します。                                                             |
| 4   | **CAccelerometerDevice::InitializeDevice**  | **CSensorDevice::Initialize**                                      | 加速度計のデバイス オブジェクトを初期化します。                                                                                                     |
| 5   | **CAccelerometerDevice::InitializeRequest** | **CAccelerometerDevice::InitializeDevice**                         | (ドライバーが以前に取得されるリソース ハブ パスと接続 ID を使用して) SPB 要求オブジェクトの初期化プロセスを開始します。 |
| 6   | **CSpbRequest::Initialize**                 | **CAccelerometerDevice::InitializeRequest**                        | 基になる SPB へのファイル ハンドルを開く                                                                                                        |

 

### <a name="initializing-the-supported-sensor-properties-and-data-fields"></a>サポートされているセンサーのプロパティとデータ フィールドの初期化

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SpbRequest.cpp          | CSpbRequest          |

 

以下の方法は、初期化プロパティとセンサーでサポートされているデータ フィールドを取得中に、ドライバーによって呼び出されます。 Windows センサー プラットフォームでは、加速度計プロパティは、読み取りまたは読み取り/書き込みのセンサーのレポート間隔や、最小のサポートされているレポートの間隔などのデータに対応します。 データ フィールドは、その x、Y、および z 軸に沿って加速度計の実際の測定値に対応します。 (このシーケンスの最初の 3 つのメソッドは、前のデータ接続、および SPB の要求オブジェクトのシーケンスの最初の 3 つのメソッドと同じことに注意してください)。

|     | メソッド                                             | によって呼び出されます                                                         | 目的                                                                                                               |
|-----|----------------------------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | 特定のデバイスがアクセスできるようにするドライバーが必要な操作を開始します。                                     |
| 2   | **CSensorDdi::Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 作成し、センサー デバイス オブジェクトを初期化します。                                                                      |
| 3   | **CSensorDevice::Initialize**                      | **CSensorDdi::Initialize**                                         | センサー ドライバー インターフェイス、クライアント マネージャー、およびレポート マネージャーを初期化します。                                  |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice::Initialize**                                      | 初期化を開始、 **IPortableDeviceValues**プロパティのキーとデータ フィールドの値を格納するオブジェクト。 |
| 5   | **CSensorDevice::AddPropertyKeys**                 | **CSensorDevice::InitializeSensorDriverInterface**                 | サポートされているプロパティを反復処理し、追加、 **PROPERTYKEY**ごと。                                        |
| 6   | **CAccelerometerDevice::GetSupportedProperties**   | **CSensorDevice::AddPropertyKeys**                                 | 取得、 **PROPERTYKEY**構造体が特定のデバイスのプロパティ。                                                |
| 7   | **CSensorDevice::AddDataFieldKeys**                | **CSensorDevice::InitializeSensorDriverInterface**                 | サポートされているデータ フィールドを反復処理し、追加、 **PROPERTYKEY**ごと。                                       |
| 8   | **CSensorDevice::GetSupportedDataFields**          | **CSensorDevice::AddDataFieldKeys**                                | 取得、 **PROPERTYKEY**の特定のデバイスのデータ フィールド。                                                         |

 

### <a name="initializing-the-persistent-unique-id-property"></a>永続的な一意の ID プロパティの初期化

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

以下の方法は、センサーの永続的な一意の識別子 (PUID) を初期化するために初期化中に、ドライバーによって呼び出されます。 Windows を使用して、 **PUID**デバイス セッション間でデータを保持します。 (このシーケンスの最初の 4 つのメソッドは、前のプロパティとデータ フィールドのシーケンスの最初の 4 つのメソッドと同じことに注意してください)。

|     | メソッド                                             | によって呼び出されます                                                         | 目的                                                                                                   |
|-----|----------------------------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | 特定のデバイスがアクセスできるようにするドライバーが必要な操作を開始します。                         |
| 2   | **CSensorDdi::Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 作成し、センサー デバイス オブジェクトを初期化します。                                                          |
| 3   | **CSensorDevice::Initialize**                      | **CSensorDdi::Initialize**                                         | センサー ドライバー インターフェイス、クライアント マネージャー、およびレポート マネージャーを初期化します。                      |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice::Initialize**                                      | プロパティのキーとデータ フィールドの値を格納するオブジェクトの初期化を開始します。               |
| 5   | **CSensorDevice::SetUniqueID**                     | **CSensorDevice::InitializeSensorDriverInterface**                 | セッション間で永続的な一意識別子 (PUID)、ドライバーを使用してを取得するメソッドを呼び出します。 |
| 6   | **CAcclerometerDevice::GetSensorObjectID**         | **CSensorDevice::SetUniqueID**                                     | 加速度計の永続的な識別子 ("ADXL345") を取得します。                                               |

 

### <a name="setting-the-default-property-values"></a>プロパティの値の既定の設定

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

Windows のセンサー プラットフォームでは、センサーの種類の既定のプロパティ値、製造元の名前、センサーのモデル、およびシリアル番号をサポートします。 SpbAccelerometer サンプルのコードでは、ドライバーとデバイスの初期化フェーズの一環としてこれらのプロパティを設定します。 以下の方法は、初期化、加速度計の既定値を設定中に、ドライバーによって呼び出されます。 (このシーケンスの最初の 4 つのメソッドは、プロパティ設定の前のシーケンスの最初の 4 つのメソッドと同じことに注意してください)。

|     | メソッド                                             | によって呼び出されます                                                         | 目的                                                                                           |
|-----|----------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | 特定のデバイスがアクセスできるようにするドライバーが必要な操作を開始します。                 |
| 2   | **CSensorDdi::Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 作成し、センサー デバイス オブジェクトを初期化します。                                                   |
| 3   | **CSensorDevice::Initialize**                      | **CSensorDdi::Initialize**                                         | センサー ドライバー インターフェイス、クライアント マネージャー、およびレポート マネージャーを初期化します。              |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice::Initialize**                                      | プロパティのキーとデータ フィールドの値を格納するオブジェクトの初期化を開始します。       |
| 5   | **CAccelerometerDevice::SetDefaultPropertyValues** | **CSensorDevice::InitializeSensorDriverInterface**                 | 既定の加速度計 (製造元、モデル、シリアル番号など) のプロパティ値を設定します。 |

 

### <a name="retrieving-the-default-writeable-properties"></a>既定の書き込み可能なプロパティを取得します。

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

センサーの読み取り/書き込みプロパティは既定のプロパティの場合は true を Windows のセンサー プラットフォームが読み取り専用にサポートします。 SpbAccelerometer サンプルのコードでは、ドライバーとデバイスの初期化フェーズの一環として、書き込み可能な (または、設定可能な) 既定のプロパティの一覧を取得します。 以下の方法は、初期化、加速度計のこれらのプロパティを取得中に、ドライバーによって呼び出されます。 (このシーケンスの最初の 4 つのメソッドは、プロパティ設定の前のシーケンスの最初の 4 つのメソッドと同じことに注意してください)。

|     | メソッド                                             | によって呼び出されます                                                         | 目的                                                                                           |
|-----|----------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | ドライバーによって特定のデバイスがアクセスできるようにするために必要な操作を開始します。                  |
| 2   | **CSensorDdi::Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 作成し、センサー デバイス オブジェクトを初期化します。                                                  |
| 3   | **CSensorDevice::Initialize**                      | **CSensorDdi::Initialize**                                         | センサー ドライバー インターフェイス、クライアント マネージャー、およびレポート マネージャーを初期化します。              |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice::Initialize**                                      | プロパティのキーとデータ フィールドの値を格納するオブジェクトの初期化を開始します。       |
| 5   | **CAccelerometerDevice::SetDefaultPropertyValues** | **CSensorDevice::InitializeSensorDriverInterface**                 | 既定の加速度計 (製造元、モデル、シリアル番号など) のプロパティ値を設定します。 |

 

### <a name="activating-support-for-events"></a>イベントのサポートをアクティブ化します。

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

Windows のセンサー プラットフォームでは、イベントをサポートします。 アプリケーションは、ドライバーからの通知を取得するイベント ハンドラーを登録します。 加速度計、これらの通知は、特定の変更感度 (g 単位) を超えた場合や、現在のレポート期間の有効期限が切れるときにトリガーされます。

センサー プラットフォームでは、イベント モデルをサポートするために、ドライバーは、イベント通知を処理するスレッドをアクティブ化する必要があります。 以下の方法は、このライセンス認証を実行するために初期化中に、ドライバーによって呼び出されます。 (このシーケンスの最初の 3 つのメソッドは、いくつかの前のシーケンスの最初の 3 つのメソッドと同じことに注意してください)。

|     | メソッド                                         | によって呼び出されます                                                         | 目的                                                                              |
|-----|------------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**               | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | 特定のデバイスがアクセスできるようにするドライバーが必要な操作を開始します。    |
| 2   | **CSensorDdi::Initialize**                     | **CMyDevice::OnPrepareHardware**                                   | 作成して、センサー デバイス オブジェクトを初期化します。                                    |
| 3   | **CSensorDevice::Initialize**                  | **CSensorDdi::Initialize**                                         | センサー ドライバー インターフェイス、クライアント マネージャー、およびレポート マネージャーを初期化します。 |
| 4   | **CReportManager::Initialize**                 | **CSensorDevice::Initialize**                                      | イベントを処理するために使用されるスレッドを作成します。                                            |
| 5   | **CReportManager::ActivateDataEventingThread** | **CReportManager::Initialize**                                     | 前のメソッドによって作成されたスレッドをアクティブにします。                                 |

 

### <a name="initializing-the-class-extension"></a>クラスの拡張機能の初期化

| モジュール     | クラス/インターフェイス |
|------------|-----------------|
| Device.cpp | CMyDevice       |

 

Windows のセンサー プラットフォームには、センサー データを取得して、イベント通知の発生の標準的なメカニズムを提供するセンサー API のクラスの拡張子が付きます。 ドライバーのサンプルを呼び出す、 **ISensorClassExtension::Initialize**メソッドへの呼び出しを受信した後に、クラス拡張を初期化するために**CMyDevice::OnPrepareHardware**します。

### <a name="configuring-the-device-and-placing-it-in-standby-mode"></a>デバイスを構成して、スタンバイ モードに配置

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

デバイスとドライバーの初期化のメソッドの最後のシーケンスは、ADXL345 を構成し、スタンバイ モードに配置します。 (このシーケンスの書き込みと読み取り操作が繰り返されます複数回まで、デバイスが構成されている。)

|     | メソッド                                          | によって呼び出されます                                                         | 目的                                                                               |
|-----|-------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnD0Entry**                        | WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント)。 | システムに新しいデバイスが表示されたときに呼び出されます。                                      |
| 2   | **CSensorDdi::Start**                           | **CMyDevice::OnD0Entry**                                           | 呼び出す CSensorDevice::Start パススルー方式。                                |
| 3   | **CSensorDevice::Start**                        | **CSensorDdi::Start**                                              | デバイスの構成プロセスを開始します。                                           |
| 4   | **CAccelerometerDevice::ConfigureHardware**     | **CSensorDevice::Start**                                           | ADXL345 の指定されたレジスタに値を書き込み操作を開始します。 |
| 5   | **CAcclerometerDevice::WriteRegister**          | **CAccelerometerDevice::ConfigureHardware**                        | ADXL345 の指定されたレジスタに値を書き込み操作を開始します。 |
| 6   | **CSpbRequest::CreateAndSendWrite**             | **CAcclerometerDevice::WriteRegister**                             | I2C バス経由での書き込み要求を送信します。                                          |
| 7   | **CAcclerometerDevice::ReadRegister**           | **CAccelerometerDevice::ConfigureHardware**                        | 指定された ADXL345 レジスタから値を読み取り操作を開始します。       |
| 8   | **CSpbRequest::CreateAndSendWriteReadSequence** | **CAcclerometerDevice::ReadRegister**                              | I2C バス経由で読み取りの結果を受信します。                                           |
| 9   | **CSpbRequest::CreateAndSendIoctl**             | **CSpbRequest::CreateAndSendWriteReadSequence**                    | ヘルパー メソッドを作成、IOCTL 要求を送信します。                                |

 

デバイスの構成作業のほとんどは、一連の行わ**CAccelerometerDevice::WriteRegister**と**CAccelerometerDevice::ReadRegister**メソッドの呼び出し。 ドライバーを使用して、::**WriteRegister** 、ADXL345 のいずれかに値を記述するメソッドを登録します対応の戻り値を確認し、::**ReadRegister**ことを確認するメソッドの書き込み。操作に成功しました。 書き込みと読み取り操作の完全なシーケンスを次に示します。

|     | メソッド                                  | 登録する | データ                | 目的                                                                                                            |
|-----|-----------------------------------------|----------|---------------------|--------------------------------------------------------------------------------------------------------------------|
| 1   | **CAccelerometerDevice::WriteRegister** | **0x2d** | **'\\0' (0x00)**    | センサーの電源管理の登録とスタンバイ モードで、デバイスをリセットします。                                   |
| 2   | **CAccelerometerDevice::ReadRegister**  | **0x2d** | **'\\0' (0x00)**    | 返されたレジスタの値は、書き込み操作が成功したことを示します。                                          |
| 3   | **CAccelerometerDevice::WriteRegister** | **0x31** | **'\\v' (0x0b)**    | 範囲が 16 G +/-の各軸に沿ったフル解像度モードでは、デバイスを設定します。                                   |
| 4   | **CAccelerometerDevice::ReadRegister**  | **0x31** | **'\\v' (0x0b**     | 返されたレジスタの値は、書き込み操作が成功したことを示します。                                          |
| 5   | **CAccelerometerDevice::WriteRegister** | **0x38** | **'\\0' (0x00)**    | センサーの FIFO コントロール レジスタをバイパス モードにリセットします。                                                      |
| 6   | **CAccelerometerDevice::ReadRegister**  | **0x38** | **'\\0' (0x00)**    | 返されたレジスタの値は、書き込み操作が成功したことを示します。                                          |
| 7   | **CAccelerometerDevice::WriteRegister** | **0x2C** | **'\\a' (0x07)**    | 設定、BW\_レート レジスタを低電力モードを開始します。                                                             |
| 8   | **CAccelerometerDevice::ReadRegister**  | **0x2C** | **'\\a' (0x07)**    | 返されたレジスタの値は、書き込み操作が成功したことを示します。                                          |
| 9   | **CAccelerometerDevice::WriteRegister** | **0x24** | **'\\x1' (0x01)**   | 設定、TRESH\_ACT (アクティビティしきい値) が 1 に登録します。                                                            |
| 10  | **CAccelerometerDevice::ReadRegister**  | **0x24** | **'\\x1' (0x01)**   |                                                                                                                    |
| 11  | **CAccelerometerDevice::WriteRegister** | **0x27** | **(0xf0)**          | 設定、ACT\_INACT\_CTL (アクティブまたは非アクティブ) 0xf0 に登録します。                                                       |
| 12  | **CAccelerometerDevice::ReadRegister**  | **0x27** | **(0xf0)**          | 返されたレジスタの値は、書き込み操作が成功したことを示します。                                              |
| 13  | **CAccelerometerDevice::WriteRegister** | **0x2f** | **'\\0x10' (0x10)** | 設定、INT\_マップ (割り込みマッピング) に登録します。 0x10 の値は、透かしが INT2 暗証番号 (pin) にマップされているを要求します。 |
| 14  | **CAccelerometerDevice::ReadRegister**  | **0x2f** | **'\\0x10' (0x10)** | 返されたレジスタの値は、書き込み操作が成功したことを示します。                                          |

 

ドライバーとデバイスが構成した後は、初期化シーケンスが完了し、アプリがセンサー データの受信を開始することができます。

 

 




