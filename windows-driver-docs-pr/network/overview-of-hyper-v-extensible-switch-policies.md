---
title: Hyper-V 拡張可能スイッチ ポリシーの概要
description: Hyper-V 拡張可能スイッチ ポリシーの概要
ms.assetid: 1D0AC55B-60F7-400E-A376-F3E2F7373A92
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03529154bb12011839c48f0daf6cff2ac0ca75fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385725"
---
# <a name="overview-of-hyper-v-extensible-switch-policies"></a>Hyper-V 拡張可能スイッチ ポリシーの概要


HYPER-V プラットフォームと拡張可能スイッチのインターフェイスは、拡張可能スイッチのスイッチとポートのポリシーを管理するインフラストラクチャを提供します。 これらのポリシーは、PowerShell コマンドレットと WMI ベースのアプリケーション プログラムによって管理されます。 このインフラストラクチャには、ストレージとポリシーの移行のサポートも提供します。

独立系ソフトウェア ベンダー (Isv) は、このインフラストラクチャを使用して、独自のカスタム ポリシーを登録することができます。 登録した後、これらのポリシーを検出し、組み込み HYPER-V ポリシー インターフェイスを使用して管理が可能です。 各ポート レベルまたは各スイッチ レベルでは、ポリシーのプロパティを構成できます。

カスタム ポリシーのプロパティだけでなく、HYPER-V 拡張可能スイッチのインターフェイスは、ポートごとに、スイッチごとのカスタム ポリシーのプロパティの状態情報を取得するためのインフラストラクチャを提供します。 この状態情報と呼ばれる*機能の状態*情報。

拡張可能スイッチのカスタム ポリシー データは、WMI 管理層で管理オブジェクト フォーマット (MOF) クラス定義を使用して登録されます。 ポートのカスタム ポリシーのプロパティの MOF クラスの例を次に示します。

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

WMI 管理層では、基になる拡張可能スイッチ拡張機能に転送されるときに、MOF データがシリアル化します。 MOF クラスは、HYPER-V 拡張可能スイッチの拡張機能で処理できる、対応する C 構造体をシリアル化されます。 前の例から、MOF クラスのシリアル化された C 構造体の例を次に示します。

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

この例は、MOF クラスは拡張可能スイッチ ポリシーのプロパティの対応する C の構造体にシリアル化するときに発生する次の点を示しています。

-   MOF ファイルのバージョンの定義は、上位ビットは、メジャー バージョンを含めることがあり、下位ビットは、マイナー バージョンを含めることが USHORT の値に変換されます。 バージョンは次のコードを使用してシリアル化されます。

    `  (((MajorVersion) << 8) + (MinorVersion))`

    0x0100 を @property に上記 Version("1") はシリアル化するなど、`(((1) << 8) + (0))`します。 バージョン (「1.1」) はを通じて 0x0101 の値にシリアル化する`(((1) << 8) + (1))`します。

    カスタム ポリシーのプロパティが、基になる拡張機能に発行されたときに、 **PropertyVersion**ポリシーのプロパティを定義する構造体のメンバーには、シリアル化されたバージョンの値が含まれています。

    オブジェクト識別子 (OID) 要求を発行したときなど、拡張可能スイッチ インターフェイス[OID\_切り替える\_ポート\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)OID は、に関連付け[**NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)構造体。 **PropertyVersion**その構造体のメンバーには、シリアル化されたバージョンの値が含まれています。

-   シリアル化された C 構造体を格納しているバッファー内のオフセットには、すべての可変長文字列がシリアル化します。 それぞれの可変長文字列として書式設定、**変数\_長さ\_文字列**このバッファーのオフセット内の構造。

 

 





