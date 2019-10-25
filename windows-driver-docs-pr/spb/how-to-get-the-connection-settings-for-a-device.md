---
title: デバイスの接続設定を取得する方法
description: SPB コントローラードライバーが EvtSpbTargetConnect コールバック関数を登録する場合、SP のクライアント (周辺ドライバー) が IRP_MJ_CREATE 要求を送信してターゲットへの論理接続を開くと、SPB フレームワーク拡張機能 (SpbCx) がこの関数を呼び出します。バス上のデバイス。 EvtSpbTargetConnect コールバックへの応答として、SPB コントローラードライバーは、ターゲットデバイスの接続設定を取得するために、SpbTargetGetConnectionParameters メソッドを呼び出す必要があります。 SPB コントローラードライバーはこれらの設定を保存し、後でクライアントからの i/o 要求に応答してデバイスにアクセスするために使用します。
ms.assetid: B614993A-0EA9-4B91-A336-80EEF9BE3E69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cc63d5fa2d9db71420b1f2f4d9043f7429fa78d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843607"
---
# <a name="how-to-get-the-connection-settings-for-a-device"></a>デバイスの接続設定を取得する方法


SPB コントローラードライバーが[*Evtspbtargetconnect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect)コールバック関数を登録した場合、この[関数は、](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)コントローラーのクライアント (周辺ドライバー) が[**IRP\_\_MJ を送信したときに、この関数を呼び出します。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)バス上のターゲットデバイスへの論理接続を開くように要求します。 *Evtspbtargetconnect*コールバックへの応答として、SPB コントローラードライバーは、ターゲットデバイスの接続設定を取得するために、 [**Spbtargetgetconnectionparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters)メソッドを呼び出す必要があります。 SPB コントローラードライバーはこれらの設定を保存し、後でクライアントからの i/o 要求に応答してデバイスにアクセスするために使用します。

たとえば、I2C バス上のターゲットデバイスの接続設定には、デバイスのバスアドレス、アドレスの幅 (7 または10ビット)、およびデバイスのアクセス時に使用するバスクロック周波数が含まれます。 I2C コントローラードライバーは、これらの設定を使用して、I2C バスを介してデバイスにアクセスするようにコントローラーを構成します。

SPB コントローラードライバーは、 **Spbtargetgetconnectionparameters**を呼び出して、*シリアルバス接続記述子*へのポインターを取得します。これは、ターゲットデバイスと型 I2C または SPI のシリアルバスへの接続を表します。 この記述子には、両方の種類のシリアルバスに共通する接続情報が含まれており、その後に、デバイスが接続されているシリアルバスに固有の情報が続きます。 この記述子の形式の詳細については、 [ACPI 5.0 の仕様](https://uefi.org/specifications)を参照してください。

次のコード例では、I2C コントローラードライバーによって、 **scsi\_i2c\_シリアル\_バス\_記述子**構造体が定義されています。 この構造体は、 *i2c シリアルバス接続記述子*を表します。これは、i2c バスに固有の接続設定が続くシリアルバス接続記述子を表すために、ACPI 5.0 仕様で使用される用語です。 **Pnp\_I2C\_serial\_BUS\_記述子**構造体の最初のメンバーである**SerialBusDescriptor**は、シリアルバスを表す[**pnp\_シリアル\_バス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/reshub/ns-reshub-_pnp_serial_bus_descriptor)の構造体です。接続記述子。 **Connectionspeed**メンバーと**SlaveAddress**メンバーには、I2C 固有の接続設定が含まれています。

```cpp
#include <reshub.h>
#include <pshpack1.h>  

//
// See the ACPI 5.0 spec, section 6.4.3.8.2.1 (I2C Serial Bus Connection Descriptor).  
//
typedef struct _PNP_I2C_SERIAL_BUS_DESCRIPTOR {  
    PNP_SERIAL_BUS_DESCRIPTOR SerialBusDescriptor;  
    ULONG ConnectionSpeed;  
    USHORT SlaveAddress;  
    // Followed by optional vendor-specific data.
    // Followed by name of serial bus controller.
} PNP_I2C_SERIAL_BUS_DESCRIPTOR, *PPNP_I2C_SERIAL_BUS_DESCRIPTOR;  
  
#include <poppack.h>
```

Reshub ヘッダーファイルは、 **PNP\_SERIAL\_BUS\_記述子**構造体を定義します。 Pshpack1 ヘッダーファイルと poppack .h ヘッダーファイルは、コンパイラによって使用される構造体の配置モードを制御します。

I2C serial bus 接続記述子は、隣接するフィールドがギャップのない、最も近いバイト境界にアラインされる、パックされたデータ構造です。 その結果、この記述子の16ビット整数値は、奇数バイト境界で開始される場合があります。 前のコード例では、隣接する構造体のメンバーをパックするようにコンパイラに指示するために pshpack1 が含まれています。また、poppack. h は、既定の構造体の配置を再開するようにコンパイラに指示します。

**PNP\_i2c\_SERIAL\_BUS\_記述子**構造体の**connectionspeed**メンバーは、ターゲットデバイスへのアクセス中に i2c バスをクロックする頻度をヘルツ単位で指定します。 **SlaveAddress**メンバーはターゲットデバイスのバスアドレスです。 一部の I2C コントローラードライバーでは、 **SlaveAddress**メンバーの後にベンダー固有のオプションのデータが続きますが、このデータはこのコード例のドライバーでは使用されないため、構造体の定義の一部ではありません。

次のコード例では、前の例の I2C コントローラードライバーが、 [**Spbtargetgetconnectionparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters)を呼び出して、i2c バス上のターゲットデバイスの接続設定を取得する `GetTargetSettings` ルーチンを実装しています。 このルーチンの*ターゲット*の入力パラメーターは、ターゲットデバイスへのハンドルです。 *設定*の出力パラメーターは、ドライバーによって割り当てられた[**SPB\_接続\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/ns-spbcx-_spb_connection_parameters)構造へのポインターであり、ルーチンは一連の接続パラメーターを書き込みます。 これらのパラメーターには、要求された接続設定へのポインターが含まれます。

```cpp
#define I2C_SERIAL_BUS_TYPE 0x01
#define I2C_SERIAL_BUS_SPECIFIC_FLAG_10BIT_ADDRESS 0x0001

typedef enum _I2C_ADDRESS_MODE
{
    AddressMode7Bit,
    AddressMode10Bit
} I2C_ADDRESS_MODE, *PI2C_ADDRESS_MODE;
  
typedef struct _I2C_TARGET_SETTINGS
{
    ULONG  ClockFrequency;
    ULONG  Address;
    I2C_ADDRESS_MODE  AddressMode;
} I2C_TARGET_SETTINGS, *PI2C_TARGET_SETTINGS;

NTSTATUS
GetTargetSettings(_In_ SPBTARGET Target, _Out_ PI2C_TARGET_SETTINGS Settings)
{
    PRH_QUERY_CONNECTION_PROPERTIES_OUTPUT_BUFFER Connection = NULL;
    SPB_CONNECTION_PARAMETERS Params;

    SPB_CONNECTION_PARAMETERS_INIT(&Params);
    SpbTargetGetConnectionParameters(Target, &Params);
    Connection = (PRH_QUERY_CONNECTION_PROPERTIES_OUTPUT_BUFFER)Params.ConnectionParameters;
    if (Connection->PropertiesLength < sizeof(PNP_SERIAL_BUS_DESCRIPTOR))
    {
        return STATUS_INVALID_PARAMETER;
    }

    PPNP_SERIAL_BUS_DESCRIPTOR Descriptor;

    Descriptor = (PPNP_SERIAL_BUS_DESCRIPTOR)Connection->ConnectionProperties;
    if (Descriptor->Tag != SERIAL_BUS_DESCRIPTOR ||
        Descriptor->SerialBusType != I2C_SERIAL_BUS_TYPE)
    {
        return STATUS_INVALID_PARAMETER;
    }

    PPNP_I2C_SERIAL_BUS_DESCRIPTOR I2CDescriptor;
    USHORT I2CFlags;

    I2CDescriptor = (PPNP_I2C_SERIAL_BUS_DESCRIPTOR)Connection->ConnectionProperties;
    Settings->Address = (ULONG)I2CDescriptor->SlaveAddress;
    I2CFlags = I2CDescriptor->SerialBusDescriptor.TypeSpecificFlags;
    Settings->AddressMode = 
                ((I2CFlags & I2C_SERIAL_BUS_SPECIFIC_FLAG_10BIT_ADDRESS) == 0) ? AddressMode7Bit : AddressMode10Bit;

    Settings->ClockFrequency = I2CDescriptor->ConnectionSpeed;

    return STATUS_SUCCESS;
}
```

前のコード例では、 [**Spbtargetgetconnectionparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters)は、接続パラメーターをドライバーによって割り当てられた `Params` 構造体に書き込みます。 `Params` の**Connectionparameters**メンバーは、 [**RH\_クエリ\_接続\_プロパティ\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/reshub/ns-reshub-_rh_query_connection_properties_output_buffer)構造 (reshub で定義) を指します。これは、 **connectionparameters**メンバーがです。シリアルバス接続記述子の最初のバイト。この記述子の残りのバイトは、 **connectionproperties**メンバーの直後に続きます。 `Params` の**Connectionparameters**メンバーによってポイントされているバッファーは、 **RH\_クエリ\_接続\_プロパティ**を格納するのに十分な大きさです。出力\_バッファー構造に加え、記述子バイトを格納します。この構造に従います。

前のコード例のドライバーによって実装された `GetTargetSettings` ルーチンは、 **Spbtargetgetconnectionparameters**から受け取った接続パラメーターに対して次のパラメーターチェックを実行します。

-   [**RH\_クエリ\_接続\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/reshub/ns-reshub-_rh_query_connection_properties_output_buffer)に含まれているシリアルバス接続記述子のサイズが、プロパティ\_出力\_バッファー構造に含まれていることを確認します。 **_ BUS\_記述子**)。
-   ACPI 5.0 仕様の要件に従って、シリアルバス接続記述子の最初のバイトがシリアル\_バス\_記述子 (定数値 0x8e) に設定されていることを確認します。
-   シリアルバス接続記述子のシリアルバスの種類が、i2c としてシリアルバスの種類を識別する\_SERIAL\_BUS\_TYPE (定数値 0x01) に設定されていることを確認します。

前のコード例の最後で、\*`Settings` 構造には、ターゲットデバイスの接続設定 (バスアドレス、アドレスの幅、およびバスクロックの頻度) が含まれています。 I2C コントローラードライバーは、これらの接続設定を使用して、デバイスにアクセスするコントローラーを構成します。

 

 




