---
title: WDI メッセージ構造
description: このセクションは、WDI コマンド メッセージの構造を説明します。
ms.assetid: 09663C5F-A458-479F-B450-A994486A6C18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16859876b0bf381c6b46f36d6d0aa7e54643b90a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346630"
---
# <a name="wdi-message-structure"></a>WDI メッセージ構造


WDI コマンドのすべてのメッセージが始まり、 [ **WDI\_メッセージ\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/dn926074)構造体。 コマンドのヘッダーには、0 個以上の型 (TLV) を値構造体が続きます。

コマンド メッセージ Id には、Wi-fi デバイスに、ホストから送信されたメッセージに記載されているが定義されている[WDI タスク Oid](https://msdn.microsoft.com/library/windows/hardware/dn926082)、 [WDI プロパティ Oid](https://msdn.microsoft.com/library/windows/hardware/dn926079)、および[WDI 状態インジケーター](https://msdn.microsoft.com/library/windows/hardware/dn926080)します。

## <a name="tlvs"></a>TLVs


TLVs の構造は、次の表で定義されます。 TLVs 内のデータでは、リトル エンディアン バイト順でします。

| フィールド                      | 種類     | 説明                                                                                                                                   |
|----------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| 種類                       | UINT16   | TLV 構造体の型。 エラーをトリガーすることがなく TLV 型が認識されないをスキップする必要があります。                                              |
| 値のバッファーの長さ | UINT16   | (バイト単位) の値のバッファーのサイズ。                                                                                                        |
| Value                      | バイト\[\] | ペイロード バッファー、構造体、構造体のリストまたはその他の TLVs に含めることができます。 データのサイズは、必要な長さを正確に一致する必要があります。 |

 

TLV グループの 2 種類があります。 静的にサイズの TLV リスト、およびマルチ TLV グループ。

## <a name="statically-sized-tlv-lists"></a>静的に TLV リストのサイズ


TLV リスト サイズが静的ににはは、いくつかのサイズを静的にメンバーが含まれます。 標準の C スタイル配列に似ています。

この例で[ **WDI\_TLV\_ユニキャスト\_アルゴリズム\_一覧**](https://msdn.microsoft.com/library/windows/hardware/dn898073) WDI のリストとして定義されて\_ALGO\_ペア.

|        |                                    |
|--------|------------------------------------|
| 種類   | WDI\_TLV\_ユニキャスト\_アルゴリズム\_一覧 |
| 長さ | N \* sizeof (WDI\_ALGO\_ペア)      |
| Value  | WDI\_ALGO\_ペア\[N\]              |

 

この使用法は、配列表記と TLV リファレンス トピックで指定されます。

## <a name="multi-tlv-groups"></a>マルチ TLV グループ


指定したオブジェクトのサイズが事前に認識されていない場合は、マルチ TLV グループが使用されます。 この使用パターンでは、N 別の可変サイズ TLVs は、指定したバッファー内で予想されるを指定します。 (N) のエントリの数は、前もってが不明し、一致する TLVs で指定されたバッファーの数によって推論されます。

この例では、親のバッファーは、 [ **WDI\_メッセージ\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/dn926074)、TLV バッファーの末尾を定義します。 なお[ **WDI\_TLV\_BSS\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn926162)親バッファー内の他のさまざまな TLV 型の間で混在させることがあります。

| Offset                         | フィールド                       | 種類                |
|--------------------------------|-----------------------------|---------------------|
| 0                              | WDI\_メッセージ\_ヘッダー        | メッセージ ヘッダー      |
| sizeof (WDI\_メッセージ\_ヘッダー)   | TLV₀ (WDI\_TLV\_BSS\_エントリ) | WDI\_BSS\_エントリ     |
| TLV₀ + L₀ sizeof (TLV ヘッダー) | TLV₁ (WDI\_TLV\_BSS\_エントリ) | WDI\_BSS\_エントリ     |
| TLV₁ + L₁ sizeof (TLV ヘッダー) | TLV₂ (WDI\_TLV\_BSS\_エントリ) | WDI\_BSS\_エントリ     |
| TLV₂ + L₂ sizeof (TLV ヘッダー) | TLV₃ (OTHER\_TLV\_型)     | その他の種類の TLV |
| TLV₃ + L₃ sizeof (TLV ヘッダー) | TLV₄ (WDI\_TLV\_BSS\_エントリ) | WDI\_BSS\_エントリ     |

 

その他の TLVs が含まれている TLVs、TLV 参照トピックは、ある、*許可されている複数の TLV インスタンス*列。 この列がチェックされ、複数回出現する指定の TLV が許可されます。 これの例は、次を参照してください。 [ **WDI\_TLV\_CONNECT\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn926266)します。

 

 





