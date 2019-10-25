---
title: Hyper-V 拡張可能スイッチ ポリシーの概要
description: Hyper-V 拡張可能スイッチ ポリシーの概要
ms.assetid: 1D0AC55B-60F7-400E-A376-F3E2F7373A92
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2243cb0d13640e10393b6a2aabd41cb4dd6f94b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843743"
---
# <a name="overview-of-hyper-v-extensible-switch-policies"></a>Hyper-V 拡張可能スイッチ ポリシーの概要


Hyper-v プラットフォームと拡張可能スイッチインターフェイスは、拡張可能スイッチのスイッチとポートポリシーを管理するためのインフラストラクチャを提供します。 これらのポリシーは、PowerShell コマンドレットと WMI ベースのアプリケーションプログラムによって管理されます。 また、このインフラストラクチャでは、ポリシーの保存と移行もサポートされています。

独立系ソフトウェアベンダー (Isv) は、このインフラストラクチャを使用して、独自のカスタムポリシーを登録できます。 これらのポリシーは、登録後に、組み込みの Hyper-v ポリシーインターフェイスを使用して検出および管理できます。 ポリシーのプロパティは、ポートごとのレベルまたはスイッチごとのレベルのいずれかで構成できます。

カスタムポリシープロパティに加えて、Hyper-v 拡張可能スイッチインターフェイスは、ポートごとまたはスイッチごとにカスタムポリシープロパティのステータス情報を取得するためのインフラストラクチャを提供します。 この状態情報は、*機能状態*情報として知られています。

拡張可能なスイッチカスタムポリシーデータは、管理オブジェクトフォーマット (MOF) クラス定義を使用して、WMI 管理層に登録されます。 カスタムポートポリシープロパティの MOF クラスの例を次に示します。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic, 
 UUID("F2F73F23-2B8E-457a-96C4-F541201C9150"),
 ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
 Provider("VmmsWmiInstanceAndMethodProvider"), 
 Locale(0x409),
 InterfaceVersion("1"),
 InterfaceRevision("0"),
DisplayName("VendorName Port Settings Friendly Name") : Amended,
Description("VendorName Port Settings detailed description.") : Amended]
class Vendor_SampleFeatureSettingData: Msvm_EthernetSwitchPortFeatureSettingDataMsvm
{
  [WmiDataId(1),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint8  IntValue8 = 0;

  [WmiDataId(2),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint16 IntValue16 = 0;

  [WmiDataId(3),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint32 IntValue32 = 0;

  [WmiDataId(4),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint64 IntValue64 = 0;

  [WmiDataId(5),
   InterfaceVersion("1"),
   InterfaceRevision("0"), 
   MaxLen(255)]
  string FixedLengthString = "";

  [WmiDataId(6),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  string VariableLengthString = "";

  [WmiDataId(7),
   InterfaceVersion("1"),
   InterfaceRevision("0"),
   Max(8)]
  uint32 FixedLengthArray[] = {};

  [WmiDataId(8),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint32 VariableLengthArray[] = {};

};
```

WMI 管理層は、基になる拡張可能なスイッチ拡張機能に転送されるときに MOF データをシリアル化します。 MOF クラスは、Hyper-v 拡張可能スイッチ拡張機能によって処理できる、対応する C 構造体にシリアル化されます。 前の例の MOF クラス用にシリアル化された C 構造体の例を次に示します。

```C++
#pragma pack(8)

typedef struct _VARIABLE_LENGTH_ARRAY
{
    UINT32 Buffer[1];
} VARIABLE_LENGTH_ARRAY;

typedef struct _SAMPLE_FEATURE_SETTINGS
{
    UINT8  IntValue8;
    UINT32 IntValue16;
    UINT32 IntValue32;
    UINT64 IntValue64;
    UINT16 FixedLengthStringByteCount;
    WCHAR  FixedLengthString[256]; 
    UINT32 VariableLengthStringOffset;    // offset to VARIABLE_LENGTH_STRING structure
    UINT32 FixedLengthArrayElementCount;
    UINT32 FixedLengthArray[8];
    UINT32 VariableLengthArrayElementCount;
    UINT32 VariableLengthArrayOffset;   // offset to VARIABLE_LENGTH_ARRAY
} SAMPLE_FEATURE_SETTINGS;
 
typedef struct _VARIABLE_LENGTH_STRING
{
    USHORT StringLength;
    WCHAR  StringBuffer[1];
} VARIABLE_LENGTH_STRING;
```

この例では、拡張可能なスイッチポリシープロパティの対応する C 構造体に MOF クラスをシリアル化するときに発生する次の点を強調しています。

-   MOF ファイルのバージョン定義は、USHORT 値に変換されます。この値は、上位ビットにメジャーバージョンが含まれ、下位ビットにマイナーバージョンが含まれています。 バージョンは、次のコードを使用してシリアル化されます。

    `  (((MajorVersion) << 8) + (MinorVersion))`

    たとえば、上のバージョン ("1") は `(((1) << 8) + (0))`を通じて0x0100 の値にシリアル化されます。 バージョン ("1.1") は `(((1) << 8) + (1))`から0x0101 の値にシリアル化されます。

    基になる拡張機能に対してカスタムポリシープロパティが発行されると、ポリシープロパティを定義する構造体の**propertyversion**メンバーは、シリアル化されたバージョンの値を格納します。

    たとえば、拡張可能なスイッチインターフェイスが Oid\_のオブジェクト識別子 (OID) 要求を発行すると[\_ポート\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)された場合、Oid は[**NDIS\_スイッチ\_ポートに関連付けられ\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)構造体。 この構造体の**Propertyversion**メンバーには、シリアル化されたバージョンの値が含まれています。

-   すべての可変長文字列は、シリアル化された C 構造体を格納するバッファー内のオフセットにシリアル化されます。 各可変長文字列は、このバッファーオフセット内の**文字列構造\_長さ\_変数**として書式設定されます。

 

 





