---
title: WDI メッセージ構造
description: ここでは、WDI コマンドメッセージの構造について説明します。
ms.assetid: 09663C5F-A458-479F-B450-A994486A6C18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37dec4615ef9bcf25e9db8396841f6380f09a1c6
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967899"
---
# <a name="wdi-message-structure"></a>WDI メッセージ構造


すべての WDI コマンドメッセージは、 [**WDI \_ メッセージ \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)構造で始まる必要があります。 Command ヘッダーの後には、0個以上の型指定値 (TLV) 構造体が続きます。

ホストから Wi-fi デバイスに送信されるメッセージに対して定義されているコマンドメッセージ Id は、「 [WDI Task oid](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-task-oids)」、「 [WDI Property oid](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-property-oids)」、および「 [WDI Status 兆候](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-status-indications)」に記載されています。

## <a name="tlvs"></a>TLVs


TLVs の構造は、次の表で定義されています。 TLVs のデータは、リトルエンディアンのバイト順です。

| フィールド                      | Type     | 説明                                                                                                                                   |
|----------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| 種類                       | UINT16   | TLV 構造体の型。 認識されない TLV 型は、エラーをトリガーせずにスキップする必要があります。                                              |
| 値バッファーの長さ | UINT16   | 値バッファーのサイズ (バイト単位)。                                                                                                        |
| 値                      | バイト\[\] | 構造体、構造体のリスト、またはその他の TLVs を含むペイロードバッファー。 データサイズは、予期された長さと正確に一致する必要があります。 |

 

TLV のグループ化には、静的にサイズ設定された TLV リストとマルチ TLV グループの2種類があります。

## <a name="statically-sized-tlv-lists"></a>静的にサイズ設定された TLV リスト


静的にサイズ設定された TLV リストには、静的なサイズのメンバーがいくつか含まれます これらは、標準 C スタイル配列に似ています。

この例では、 [**WDI \_ TLV \_ ユニキャスト \_ アルゴリズムの \_ 一覧**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-unicast-algorithm-list)が WDI algo のペアの一覧として定義されてい \_ \_ ます。

**種類**: WDI \_ TLV \_ ユニキャスト \_ アルゴリズムの \_ 一覧

**長さ**: N \* sizeof (WDI \_ algo の \_ ペア)

**値**: WDI \_ algo の \_ ペア \[ N\]


 

この使用法は、配列表記の TLV 参照トピックで指定されています。

## <a name="multi-tlv-groups"></a>複数の TLV グループ


特定のオブジェクトのサイズが事前にわかっていない場合は、マルチ TLV グループが使用されます。 この使用パターンでは、指定されたバッファー内で、N 異なる可変サイズ TLVs が想定されていることを指定します。 エントリの数 (N) はあらかじめわかっていません。また、指定されたバッファーの一致する TLVs の数によって推論されます。

この例では、親バッファーは[**WDI \_ MESSAGE \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)で、TLV バッファーの末尾を定義します。 [**WDI \_ TLV \_ BSS \_ エントリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry)は、親バッファー内の他の異なる TLV 型の間に散在している可能性があることに注意してください。

| Offset                         | フィールド                       | Type                |
|--------------------------------|-----------------------------|---------------------|
| 0                              | WDI \_ メッセージ \_ ヘッダー        | メッセージ ヘッダー      |
| sizeof (WDI \_ MESSAGE \_ HEADER)   | TLV ₀ (WDI \_ TLV \_ BSS \_ エントリ) | WDI \_ BSS \_ エントリ     |
| TLV ₀ + L ₀ + sizeof (TLV Header) | TLV ₁ (WDI \_ TLV \_ BSS \_ エントリ) | WDI \_ BSS \_ エントリ     |
| TLV ₁ + L ₁ + sizeof (TLV Header) | TLV ₂ (WDI \_ TLV \_ BSS \_ エントリ) | WDI \_ BSS \_ エントリ     |
| TLV ₂ + L ₂ + sizeof (TLV Header) | TLV ₃ (その他の \_ TLV \_ 型)     | その他の TLV 型 |
| TLV ₃ + L ₃ + sizeof (TLV Header) | TLV ₄ (WDI \_ TLV \_ BSS \_ エントリ) | WDI \_ BSS \_ エントリ     |

 

TLVs に他の TLVs が含まれている場合、TLV の参照トピックでは、*複数の TLV instances が許可さ*れた列があります。 この列をオンにすると、指定した TLV が複数回出現することが許可されます。 この例については、「 [**WDI \_ TLV \_ CONNECT \_ PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connect-parameters)」を参照してください。

 

 





