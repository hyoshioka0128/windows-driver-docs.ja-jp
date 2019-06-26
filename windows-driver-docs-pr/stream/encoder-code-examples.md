---
title: エンコーダーのコード例
description: エンコーダーのコード例
ms.assetid: cbe773ad-2222-4d62-8e1e-6d47418a3e7c
keywords:
- 可変ビット レートの WDK エンコーダー
- エンコーダー デバイス WDK AVStream
- AVStream WDK、エンコーダーのデバイス
- 非圧縮データ ストリームの WDK AVStream
- エンコードされたストリーム WDK AVStream
- オーディオ エンコーダー デバイス WDK AVStream
- ビデオ エンコーダー デバイス WDK AVStream
- ENCAPIPARAM_BITRATE_MODE
- ENCAPIPARAM_BITRATE
- ビット レートの WDK エンコーダー
- レジストリの WDK エンコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9702527288d70bf306dca1418df99fe79b4c7b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384125"
---
# <a name="encoder-code-examples"></a>エンコーダーのコード例


次のコード例がに基づいて、 [AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)します。 次を説明します。

-   ビット レートでサポートされているエンコーダーを指定する方法

-   エンコーダーでサポートされるモードのエンコード ビット レートを指定する方法

-   Encoder デバイスの実行時にメタデータ値を指定する方法*デバイス パラメーター\\機能*レジストリ キー

### <a name="implementing-supported-bit-rates"></a>**サポートされているビット レートを実装します。**

次のコード スニペットは、サポートを実装する方法を示します、 [ENCAPIPARAM\_ビットレート](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate)プロパティ。 使用して、 [ **KSPROPERTY\_ステッピング\_長い**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_stepping_long) 400 bps 下限の境界と大きく 4,000,000 bps 上限を 400 ビット/秒 (bps) のステップ実行の粒度を指定する構造体。

```cpp
const KSPROPERTY_STEPPING_LONG BitRateRanges [] = {
    {
        400,
        0,
        400,
        4000000
    }
};
```

GraphEdit などのツールでのフィルターを右クリックして、エンコーダーのフィルターのプロパティ ページにアクセスする場合が表示されます、**ビット レート**スライダー バーをこれらの値が使用されます。

次に、既定のインスタンスの作成時にエンコーダーのフィルターのビット レートをエンコードを指定します。 使用するデータ型は、ENCAPIPARAM で必要なプロパティ値の型に対応する ULONG\_ビットレート プロパティ。 この値は、既定のエンコード「ビット レート」、エンコーダーのプロパティ ページに表示されます。

```cpp
const ULONG BitRateValues [] = {
    1000000
};
```

法律の範囲と既定値のリストを指定して、ENCAPIPARAM の\_ビットレート プロパティ。

```cpp
 const KSPROPERTY_MEMBERSLIST BitRateMembersList [] = {
    {
        {
            KSPROPERTY_MEMBER_STEPPEDRANGES,
            sizeof (BitRateRanges),
            SIZEOF_ARRAY (BitRateRanges),
            0
        },
        BitRateRanges
    },
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateValues),
            SIZEOF_ARRAY (BitRateValues),
            KSPROPERTY_MEMBER_FLAG_DEFAULT
        },
        BitRateValues
    }
};
```

```cpp
 const KSPROPERTY_VALUES BitRateValuesSet = {
    {
        STATICGUIDOF (KSPROPTYPESETID_General),
        VT_UI4,
        0
    },
    SIZEOF_ARRAY (BitRateMembersList),
    BitRateMembersList
};
```

ENCAPIPARAM に対して定義されている 1 つのプロパティを指定\_ビットレート プロパティのセット。

```cpp
DEFINE_KSPROPERTY_TABLE(ENCAPI_BitRate) {
    DEFINE_KSPROPERTY_ITEM (
        0,
        GetBitRateHandler, //Get-property handler supported
        sizeof (KSPROPERTY),
        sizeof (ULONG),
        SetBitRateHandler, //Set-property handler supported
        &BitRateValuesSet,
        0,
        NULL,
        NULL,
        sizeof (ULONG)
        )
};
```

**注**   、*取得*-プロパティ ハンドラーがエンコード ビット レートを返します、*設定*-プロパティ ハンドラーが受信渡された値が使用する前に有効であるをテストする必要があります。

 

### <a name="implementing-supported-encoding-bit-rate-modes"></a>**エンコード ビット レートのモードをサポートを実装します。**

次のコード スニペットは、サポートを実装する方法を示します、 [ENCAPIPARAM\_ビットレート\_モード](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate-mode)プロパティ。

エンコーダーでサポートされているエンコード モードを定義します。

```cpp
 const VIDEOENCODER_BITRATE_MODE BitRateModeValues [] = {
    ConstantBitRate,
    VariableBitRateAverage
};
```

既定のエンコード ビット レート モードを平均可変ビット レートを指定します。

```cpp
const VIDEOENCODER_BITRATE_MODE BitRateModeDefaultValues [] = {
    VariableBitRateAverage
};
```

法律の範囲の一覧を指定し、既定値を ENCAPIPARAM の\_ビットレート\_モード プロパティ。

```cpp
const KSPROPERTY_MEMBERSLIST BitRateModeMembersList [] = {
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateModeValues),
            SIZEOF_ARRAY (BitRateModeValues),
            0
        },
        BitRateModeValues
    },
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateModeDefaultValues),
            SIZEOF_ARRAY (BitRateModeDefaultValues),
            KSPROPERTY_MEMBER_FLAG_DEFAULT
        },
        BitRateModeDefaultValues
    }
};

const KSPROPERTY_VALUES BitRateModeValuesSet = {
    {
        STATICGUIDOF (KSPROPTYPESETID_General),
        VT_I4,
        0
    },
    SIZEOF_ARRAY (BitRateModeMembersList),
    BitRateModeMembersList
};
```

ENCAPIPARAM に対して定義されている 1 つのプロパティを指定\_ビットレート\_モード プロパティのセット。

```cpp
DEFINE_KSPROPERTY_TABLE(ENCAPI_BitRateMode) {
    DEFINE_KSPROPERTY_ITEM (
        0,
        GetBitRateModeHandler, //Get-property handler supported
        sizeof (KSPROPERTY),
        sizeof (VIDEOENCODER_BITRATE_MODE),
        SetBitRateModeHandler, //Set-property handler supported
        &BitRateModeValuesSet,
        0,
        NULL,
        NULL,
        sizeof (VIDEOENCODER_BITRATE_MODE)
        )
};
```

**注**   、*取得*-プロパティ ハンドラーは、エンコード ビット レートのモードを返す必要があります、*設定*-プロパティ ハンドラーが受信渡された値が前に有効であるをテストする必要がありますこれを使用します。

 

プロパティ セットは、として指定し、 [ **KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)構造体のオートメーション テーブル。

```cpp
DEFINE_KSPROPERTY_SET_TABLE(PropertyTable) {
    DEFINE_KSPROPERTY_SET(
        &ENCAPIPARAM_BITRATE_MODE,
        SIZEOF_ARRAY (ENCAPI_BitRateMode),
        ENCAPI_BitRateMode,
        0,
        NULL
        ),
    DEFINE_KSPROPERTY_SET(
        &ENCAPIPARAM_BITRATE,
        SIZEOF_ARRAY (ENCAPI_BitRate),
        ENCAPI_BitRate,
        0,
        NULL
        )
};

DEFINE_KSAUTOMATION_TABLE(FilterTestTable) {
    DEFINE_KSAUTOMATION_PROPERTIES(PropertyTable),
    DEFINE_KSAUTOMATION_METHODS_NULL,
    DEFINE_KSAUTOMATION_EVENTS_NULL
};

const 
KSFILTER_DESCRIPTOR 
FilterDescriptor = {
    ...,
    &FilterTestTable, // Automation Table
    ...,
    ...
};
```

### <a href="" id="specifying-the-encoder-s-capabilities-in-the-registry"></a>**レジストリで、エンコーダーの機能を指定します。**

次のコード サンプルを作成する方法を示します、*機能*下のレジストリ キー、*デバイス パラメーター*レジストリ キー、および作成し、サブ キーと下の値を指定する方法、 *機能*キー。 ドライバーの初期化時に、このコードを実行します。

**注:** 次のコードは、物理デバイスごとの 1 つのハードウェアのエンコーダーの存在を想定しています。 かどうかは、ハードウェアには、複数のエンコーダーが含まれていますへの呼び出しで返されるリストを反復処理する必要があります、 **IoGetDeviceInterfaces**関数を各エンコーダーの機能を登録します。

```cpp
/**************************************************************************
CreateDwordValueInCapabilityRegistry()

IN Pdo: PhysicalDeviceObject
IN categoryGUID: Category GUID eg KSCATEGORY_CAPTURE

1. Get Symbolic name for interface
2. Open registry key for storing information about a 
   particular device interface instance
3. Create Capabilities key under "Device Parameters" key
4. Create a DWORD value "TestCapValueDWORD" under Capabilities

Must be running at IRQL = PASSIVE_LEVEL in the context of a system thread
**************************************************************************/
NTSTATUS CreateDwordValueInCapabilityRegistry(IN PDEVICE_OBJECT pdo, IN GUID categoryGUID)

{

    // 1. Get Symbolic name for interface
    // pSymbolicNameList can contain multiple strings if pdo is NULL. 
    // Driver should parse this list of string to get 
    // the one corresponding to current device interface instance. 
    PWSTR  pSymbolicNameList = NULL;

    NTSTATUS ntStatus = IoGetDeviceInterfaces(
        &categoryGUID,
        pdo,
        DEVICE_INTERFACE_INCLUDE_NONACTIVE,
        &pSymbolicNameList);
    if (NT_SUCCESS(ntStatus) && (NULL != pSymbolicNameList))
    {
        HANDLE hDeviceParametersKey = NULL;
        UNICODE_STRING symbolicName;

        // 2. Open registry key for storing information about a 
        // particular device interface instance
        RtlInitUnicodeString(&symbolicName, pSymbolicNameList);
        ntStatus = IoOpenDeviceInterfaceRegistryKey(
            &symbolicName,
            KEY_READ|KEY_WRITE,
            &hDeviceParametersKey);
        if (NT_SUCCESS(ntStatus))
        {
            OBJECT_ATTRIBUTES objAttribSubKey;
            UNICODE_STRING subKey;
 
            // 3. Create Capabilities key under "Device Parameters" key
            RtlInitUnicodeString(&subKey,L"Capabilities");
            InitializeObjectAttributes(&objAttribSubKey,
                &subKey,
                OBJ_KERNEL_HANDLE,
                hDeviceParametersKey,
                NULL);
 
            HANDLE hCapabilityKeyHandle = NULL;
 
            ntStatus = ZwCreateKey(&hCapabilityKeyHandle,
                    KEY_READ|KEY_WRITE|KEY_SET_VALUE,
                    &objAttribSubKey,
                    0,
                    NULL,
                    REG_OPTION_NON_VOLATILE,
                    NULL);
            if (NT_SUCCESS(ntStatus))
            {
                OBJECT_ATTRIBUTES objAttribDwordKeyVal;
                UNICODE_STRING subValDword;
 
                // 4. Create a DWORD value "TestCapValueDWORD" under Capabilities 
                RtlInitUnicodeString(&subValDword,L"TestCapValueDWORD");
 
                ULONG data = 0xaaaaaaaa;
 
                ntStatus = ZwSetValueKey(hCapabilityKeyHandle,&subValDword,0,REG_DWORD,&data,sizeof(ULONG));
                ZwClose(hCapabilityKeyHandle);
            }
        }
        ZwClose(hDeviceParametersKey);
        ExFreePool(pSymbolicNameList);
    }
 
    return ntStatus;
}
```

 

 




