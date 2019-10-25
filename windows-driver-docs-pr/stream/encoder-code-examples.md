---
title: エンコーダーのコード例
description: エンコーダーのコード例
ms.assetid: cbe773ad-2222-4d62-8e1e-6d47418a3e7c
keywords:
- 可変ビットレート WDK エンコーダー
- エンコーダーデバイス WDK AVStream
- AVStream WDK、エンコーダーデバイス
- 非圧縮データストリーム WDK AVStream
- エンコードされたストリーム WDK AVStream
- オーディオエンコーダーデバイス WDK AVStream
- ビデオエンコーダーデバイス WDK AVStream
- ENCAPIPARAM_BITRATE_MODE
- ENCAPIPARAM_BITRATE
- ビットレート WDK エンコーダー
- レジストリ WDK エンコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29f6b83cee8a47538019fbefe3cb244aab5a0e5c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843205"
---
# <a name="encoder-code-examples"></a>エンコーダーのコード例


次のコード例は、Avstream のシミュレートされた[ハードウェアサンプルドライバー (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)に基づいています。 次のことを示します。

-   エンコーダーでサポートされるビットレートを指定する方法

-   エンコーダーでサポートされるビットレートエンコードモードを指定する方法

-   エンコーダーデバイスの*デバイスパラメーター\\機能*のレジストリキーで実行時にメタデータ値を指定する方法

### <a name="implementing-supported-bit-rates"></a>**サポートされるビットレートの実装**

次のコードスニペットは、 [Encapiparam\_ビットレート](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate)プロパティのサポートを実装する方法を示しています。 Ksk プロパティを使用して、 [ **\_LONG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)構造体をステップ実行\_、400 bps の下限と 400万 bps の上限を指定して、400ビット/秒 (bps) のステッピング粒度を指定します。

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

GraphEdit などのツールでフィルターを右クリックしてエンコーダーフィルターのプロパティページにアクセスすると、これらの値が使用されている **ビットレート** スライダーバーが表示されます。

次に、エンコーダーフィルターのインスタンスが作成されたときの既定のエンコードビットレートを指定します。 使用されるデータ型は、ENCAPIPARAM\_ビットレートプロパティに必要なプロパティ値の型に対応する ULONG です。 この値は、エンコーダーのプロパティページに表示される既定のエンコード "Bit Rate" です。

```cpp
const ULONG BitRateValues [] = {
    1000000
};
```

有効な範囲の一覧と、ENCAPIPARAM\_ビットレートプロパティの既定値を指定します。

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

ENCAPIPARAM\_ビットレートプロパティセットに定義されている1つのプロパティを指定します。

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

*Get*プロパティハンドラーがエンコーディングビットレートを返し  、 *Set*プロパティハンドラーは、渡された入力値が有効であることをテストしてから使用する必要があることに**注意**してください。

 

### <a name="implementing-supported-encoding-bit-rate-modes"></a>**サポートされているエンコードビットレートモードの実装**

次のコードスニペットは、 [Encapiparam\_ビットレート\_MODE](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate-mode)プロパティのサポートを実装する方法を示しています。

エンコーダーでサポートされているエンコードモードを定義します。

```cpp
 const VIDEOENCODER_BITRATE_MODE BitRateModeValues [] = {
    ConstantBitRate,
    VariableBitRateAverage
};
```

既定のエンコードビットレートモードを平均可変ビットレートとして指定します。

```cpp
const VIDEOENCODER_BITRATE_MODE BitRateModeDefaultValues [] = {
    VariableBitRateAverage
};
```

ENCAPIPARAM\_ビットレート\_MODE プロパティの有効範囲と既定値の一覧を指定します。

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

ENCAPIPARAM\_ビットレート\_MODE プロパティセットに対して定義されている単一のプロパティを指定します。

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

*Get*プロパティハンドラーがエンコーディングビットレートモードを返す必要がある  **ことに注意**してください。また、 *Set*プロパティハンドラーは、使用前に渡された入力値が有効であることをテストする必要があります。

 

次に、プロパティセットを[**Ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造体のオートメーションテーブルとして指定します。

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

### <a href="" id="specifying-the-encoder-s-capabilities-in-the-registry"></a>**レジストリでのエンコーダーの機能の指定**

次のコードサンプルでは、*デバイスパラメーター*レジストリキーの下に*機能*のレジストリキーを作成する方法、および*機能*キーの下にサブキーと値を作成して指定する方法を示します。 ドライバーの初期化時に、このコードを実行します。

**注:** 次のコードは、物理デバイスごとに1つのハードウェアエンコーダーが存在することを前提としています。 ハードウェアに複数のエンコーダーが含まれている場合は、 **Iogetdeviceinterfaces**関数の呼び出しで返されたリストを反復処理し、各エンコーダーの機能を登録する必要があります。

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

 

 




