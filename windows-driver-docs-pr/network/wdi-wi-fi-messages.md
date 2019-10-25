---
title: WDI メッセージ構造
description: ここでは、WDI コマンドメッセージの構造について説明します。
ms.assetid: 09663C5F-A458-479F-B450-A994486A6C18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ca9f38b751258d438daf81d66f9c979e0dce47c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841706"
---
# <a name="wdi-message-structure"></a>WDI メッセージ構造


すべての WDI コマンドメッセージは、 [**WDI\_MESSAGE\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)構造体で始まる必要があります。 Command ヘッダーの後には、0個以上の型指定値 (TLV) 構造体が続きます。

ホストから Wi-fi デバイスに送信されるメッセージに対して定義されているコマンドメッセージ Id は、「 [WDI Task oid](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-task-oids)」、「 [WDI Property oid](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-property-oids)」、および「 [WDI Status 兆候](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-status-indications)」に記載されています。

## <a name="tlvs"></a>TLVs


TLVs の構造は、次の表で定義されています。 TLVs のデータは、リトルエンディアンのバイト順です。

| フィールド                      | タスクバーの検索ボックスに     | 説明                                                                                                                                   |
|----------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| タスクバーの検索ボックスに                       | UINT16   | TLV 構造体の型。 認識されない TLV 型は、エラーをトリガーせずにスキップする必要があります。                                              |
| 値バッファーの長さ | UINT16   | 値バッファーのサイズ (バイト単位)。                                                                                                        |
| Value                      | バイト\[\] | 構造体、構造体のリスト、またはその他の TLVs を含むペイロードバッファー。 データサイズは、予期された長さと正確に一致する必要があります。 |

 

TLV のグループ化には、静的にサイズ設定された TLV リストとマルチ TLV グループの2種類があります。

## <a name="statically-sized-tlv-lists"></a>静的にサイズ設定された TLV リスト


静的にサイズ設定された TLV リストには、静的なサイズのメンバーがいくつか含まれます これらは、標準 C スタイル配列に似ています。

この例では、 [**WDI\_TLV\_ユニキャスト\_アルゴリズム\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-unicast-algorithm-list)は、WDI\_algo\_のペアの一覧として定義されています。

|        |                                    |
|--------|------------------------------------|
| タスクバーの検索ボックスに   | WDI\_TLV\_ユニキャスト\_アルゴリズム\_一覧 |
| 長さ | N \* sizeof (WDI\_ALGO\_のペア)      |
| Value  | WDI\_ALGO\_ペア\[N\]              |

 

この使用法は、配列表記の TLV 参照トピックで指定されています。

## <a name="multi-tlv-groups"></a>複数の TLV グループ


特定のオブジェクトのサイズが事前にわかっていない場合は、マルチ TLV グループが使用されます。 この使用パターンでは、指定されたバッファー内で、N 異なる可変サイズ TLVs が想定されていることを指定します。 エントリの数 (N) はあらかじめわかっていません。また、指定されたバッファーの一致する TLVs の数によって推論されます。

この例では、親バッファーは、TLV バッファーの末尾を定義する[**WDI\_メッセージ\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)です。 [**WDI\_TLV\_BSS\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry)は、親バッファー内の他の異なる TLV 型の間に散在している可能性があることに注意してください。

| Offset                         | フィールド                       | タスクバーの検索ボックスに                |
|--------------------------------|-----------------------------|---------------------|
| 0                              | WDI\_メッセージ\_ヘッダー        | メッセージヘッダー      |
| sizeof (WDI\_MESSAGE\_HEADER)   | TLV ₀ (WDI\_TLV\_BSS\_ENTRY) | WDI\_BSS\_エントリ     |
| TLV ₀ + L ₀ + sizeof (TLV Header) | TLV ₁ (WDI\_TLV\_BSS\_ENTRY) | WDI\_BSS\_エントリ     |
| TLV ₁ + L ₁ + sizeof (TLV Header) | TLV ₂ (WDI\_TLV\_BSS\_ENTRY) | WDI\_BSS\_エントリ     |
| TLV ₂ + L ₂ + sizeof (TLV Header) | TLV ₃ (その他の\_TLV\_型)     | その他の TLV 型 |
| TLV ₃ + L ₃ + sizeof (TLV Header) | TLV ₄ (WDI\_TLV\_BSS\_ENTRY) | WDI\_BSS\_エントリ     |

 

TLVs に他の TLVs が含まれている場合、TLV の参照トピックでは、*複数の TLV instances が許可さ*れた列があります。 この列をオンにすると、指定した TLV が複数回出現することが許可されます。 この例については、「 [**WDI\_TLV\_CONNECT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connect-parameters)」を参照してください。

 

 





