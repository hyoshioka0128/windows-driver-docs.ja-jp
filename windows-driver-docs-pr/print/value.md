---
title: Value (WSD)
description: WSD 値構成体を使用すると、特定のスキーマ要素からデータを取得するクエリを使用して、bidi 通信スキーマを拡張できます。
ms.assetid: 8930e012-88ee-44ff-9abc-a15367f04ca3
keywords:
- 値の構成体
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 55321eb98cdf6abb3aac354dc04c2c36fe4e4ad5
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756172"
---
# <a name="value-wsd"></a>Value (WSD)

WSD コンストラクトを使用すると、 `Value` Web サービスインターフェイスの特定のスキーマ要素からデータを取得するクエリを使用して、bidi 通信スキーマを拡張できます。

| 属性 | 説明 |
|--|--|
| **drvPrinterEvent** | Optionalポートモニターがドライバーに通知を送信するかどうかを示すブール値です。 **TRUE**の値は、ポートモニターがドライバーに通知を送信することを示します。**FALSE**は、ポートモニターがドライバーに通知を送信しないことを示します。 |
| **filter** | クエリで指定された XML ドキュメントに、WSD モニターが適用する XPath クエリ。 このトピックの後半の説明を参照してください。 |
| **name** | スキーマ値の名前です。 |
| **query** | WSD モニターが実行するクエリの種類。 |
| **type** | コンストラクター内のデータの型 `Value` 。 [**BIDI_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)列挙体の値。 |
| **xmllang** | Optionalブール値。 **TRUE**の場合、関連付けられた `Value` 構造体をローカライズ可能な文字列値として扱う必要があることを意味します。 これは、上記で定義した XPath クエリで、xml: lang 属性で区別されるノードの一覧を返すことが想定されていることを意味します。 次に、WSD モニタは、値の一覧で最適なロケール一致を検索します。 既定値は**FALSE**です。 |

XPath 言語は Windows に実装されており、XML ファイル内の要素を指定する便利な方法を提供します。 詳細については、「 [XPath リファレンス](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256115(v=vs.100))」を参照してください。

**Xmllang**属性は、コンストラクトの type 属性 `Value` が "bidi \_ STRING" または "bidi TEXT" の場合にのみ使用され \_ ます。

`Value`コンストラクトは、WsdBidi で定義されています。

## <a name="example"></a>例

次のコード例では、WSD モニターによって、RAM メモリのサイズが整数値として決定されます。

```xml
<Schema xmlns:nprt='https://schemas.microsoft.com/windows/2005/05/wdp/print'>
  <Property name='Printer'>
    <Property name='DeviceInfo'>
      <Value name='PrinterString'
 query='nprt:PrinterDescription'
 filter='nprt:PrinterDescription/nprt:PrinterName'
 type='BIDI_STRING'
 xmllang='true'/>
    </Property>
    <Property name='Configuration'>
      <Property name='Memory'>
        <Value name='Size'
          query='wprt:PrinterConfiguration'
          filter='wprt:PrinterConfiguration/wprt:Storage/wprt:StorageEntry[wprt:Type="RAM"]/wprt:Size'
          type='BIDI_INT'/>
      </Property>
    </Property>
   </Property>
</Schema>
```

前の例では、次のクエリが実行されます。

```console
\Printer.DeviceInfo:PrinterString
\Printer.Configuration.Memory:Size
```
