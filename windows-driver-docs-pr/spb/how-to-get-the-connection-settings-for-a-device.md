---
title: デバイスの接続設定を取得する方法
description: SPB コント ローラーのドライバーが EvtSpbTargetConnect のコールバック関数を登録する場合、SPB フレームワークの拡張機能 (SpbCx) によってコント ローラーのクライアント (周辺ドライバー) の場合は、この関数要求を送信します irp_mj_create 用ターゲットへの論理接続を開くバス上のデバイス。 EvtSpbTargetConnect コールバックへの応答、SPB のコント ローラー ドライバーがターゲット デバイスの接続設定を取得する SpbTargetGetConnectionParameters メソッドを呼び出す必要があります。 SPB コント ローラーのドライバーでは、これらの設定を格納し、それらを後でクライアントからの I/O 要求に応答内のデバイスへのアクセスに使用します。
ms.assetid: B614993A-0EA9-4B91-A336-80EEF9BE3E69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 337e1089e103bc67e2da9b8d4ba96e1746ae4814
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553542"
---
# <a name="how-to-get-the-connection-settings-for-a-device"></a>デバイスの接続設定を取得する方法


SPB コント ローラーのドライバーを登録する場合、 [ *EvtSpbTargetConnect* ](https://msdn.microsoft.com/library/windows/hardware/hh450818)コールバック関数、 [SPB フレームワーク拡張](https://msdn.microsoft.com/library/windows/hardware/hh406203)(SpbCx) は、クライアント (ときに、この関数を呼び出す周辺機器のドライバー)、コント ローラーの送信、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff550729)バス上のターゲット デバイスへの論理接続を開く要求。 応答、 *EvtSpbTargetConnect* SPB コント ローラーのドライバーを呼び出す必要があります、コールバック、 [ **SpbTargetGetConnectionParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh450926)の接続を取得する方法ターゲット デバイスの設定です。 SPB コント ローラーのドライバーでは、これらの設定を格納し、それらを後でクライアントからの I/O 要求に応答内のデバイスへのアクセスに使用します。

たとえば、I2C バス上のターゲット デバイスの接続設定には、デバイス、アドレスの幅 (7 または 10 ビット)、およびデバイスのアクセス時に使用するバスのクロック周波数のバスのアドレスが含まれます。 I2C コント ローラーのドライバーでは、これらの設定を使用して、I2C バス経由でデバイスにアクセスするコント ローラーを構成します。

SPB のコント ローラー ドライバーは呼び出し**SpbTargetGetConnectionParameters**へのポインターを取得する、*シリアル バス接続記述子*I2C 型のシリアル バスにターゲット デバイスの接続を記述するか、SPI を示します。 この記述子には、両方シリアル バスの種類に共通であり、デバイスが接続されているシリアル バスに固有の情報が続きますされる接続情報が含まれています。 この記述子の形式の詳細については、次を参照してください。、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。

次のコード例では、I2C コント ローラーのドライバー定義、 **PNP\_I2C\_シリアル\_BUS\_記述子**構造体。 この構造体を表す、 *I2C シリアル バス接続記述子*、これは、ACPI 5.0 仕様を使用して、I2C に固有の接続設定が後に続くシリアル バス接続記述子をについて説明する用語バスです。 最初のメンバー、 **PNP\_I2C\_シリアル\_BUS\_記述子**構造、 **SerialBusDescriptor**は、 [ **PNP\_シリアル\_BUS\_記述子**](https://msdn.microsoft.com/library/windows/hardware/jj938062)シリアル バス接続記述子を表す構造体です。 **ConnectionSpeed**と**SlaveAddress**メンバー I2C に固有の接続設定を含めることができます。

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

Reshub.h ヘッダー ファイルに定義されて、 **PNP\_シリアル\_BUS\_記述子**構造体。 Pshpack1.h と poppack.h ヘッダー ファイルでは、コンパイラで使用される構造体の配置モードを制御します。

I2C シリアル バス接続記述子は、隣接するフィールドが介在する隙間なく、最も近いバイト境界に整列はパックされたデータ構造です。 その結果、この記述子の 16 ビット整数値が奇数バイトの境界で開始可能性があります。 上記のコード例では、pshpack1.h は隣接する構造体のメンバーをパックするようにコンパイラに指示する含まれており、poppack.h 既定構造体の配置を再開するようにコンパイラに指示します。

**ConnectionSpeed**のメンバー、 **PNP\_I2C\_シリアル\_BUS\_記述子**構造体では、ヘルツで、頻度を指定します。I2C バスは、ターゲット デバイスのアクセス中にクロックします。 **SlaveAddress**メンバーは、ターゲット デバイスのバスのアドレス。 I2C コント ローラーのドライバーによって、 **SlaveAddress**メンバーは、任意のベンダー固有データの後に指定可能性がありますが、このデータは、このコード例では、ドライバーによって使用されていないは、そのため、構造体の定義の一部です。

次のコード例では、I2C コント ローラー ドライバーが前の例から実装、`GetTargetSettings`ルーチンを呼び出す[ **SpbTargetGetConnectionParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh450926)接続設定を取得するにはI2C バス上のターゲット デバイス *ターゲット*このルーチンへの入力パラメーターは、ターゲット デバイスを識別するハンドル。 *設定*ドライバーに割り当てられたへのポインターに出力パラメーターが[ **SPB\_接続\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh406204)構造体、ルーチン一連の接続パラメーターを書き込みます。 これらのパラメーターには、要求された接続の設定へのポインターが含まれます。

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

上記のコード例で[ **SpbTargetGetConnectionParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh450926)接続パラメーターを書き込むドライバーに割り当てられた`Params`構造体。 **ConnectionParameters**のメンバー`Params`を指す、 [ **RH\_クエリ\_接続\_プロパティ\_出力\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/jj938063)構造 (reshub.h で定義されている) が**ConnectionProperties**メンバーがシリアルの最初のバイト バス接続記述子; この記述子の残りのバイト直後に、 **ConnectionProperties**メンバー。 によって示されるバッファー、 **ConnectionParameters**のメンバー`Params`を格納するのに十分な大きさが、 **RH\_クエリ\_接続\_プロパティ\_出力\_バッファー**さらにこの構造に従う記述子バイト構造体します。

ドライバー実装`GetTargetSettings`ルーチンが上記のコード例から受信した接続パラメーターには、次のパラメーター チェックを実行します**SpbTargetGetConnectionParameters**:。

-   シリアル バス接続記述子のサイズが含まれることを確認、 [ **RH\_クエリ\_接続\_プロパティ\_出力\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/jj938063)構造は、少なくとも**sizeof**(**PNP\_シリアル\_BUS\_記述子**)。
-   シリアル バス接続記述子の最初のバイトがシリアルに設定されていることを確認します。\_BUS\_記述子 (定数値 0x8e) ACPI 5.0 仕様で必要とします。
-   I2C にシリアル バス接続記述子のシリアル バスの種類が設定されていることを確認します。\_シリアル\_BUS\_I2C としてシリアル バスの種類を識別する型 (定数値 0x01)。

上記のコード例の最後に、 \* `Settings`構造体には、ターゲット デバイスの接続の設定 (bus アドレス、アドレスの幅とバスのクロック周波数) が含まれています。 I2C コント ローラーのドライバーでは、これらの接続設定を使用して、デバイスにアクセスするコント ローラーを構成します。

 

 




