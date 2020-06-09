---
title: リスト
description: リスト
ms.assetid: 4cf1c1ea-f890-4f9d-96ea-b79790f6bc60
keywords:
- リストコンストラクト
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0131160bf7e15d6dfece9336d374f570ca4b9e66
ms.sourcegitcommit: d71024c0c782b5c013192d960700802eafc120f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84507101"
---
# <a name="list"></a>リスト

Web Services for Devices (WSD) `List` コンストラクトは、XPath フィルタークエリによって指定されたコンマ区切りの値のリストを構成する文字列型です。 `List`コンストラクトは、WsdBidi で定義されています。

| 属性 | 説明 |
| --- | --- |
| **drvPrinterEvent** | Optionalポートモニターがドライバーに通知を送信するかどうかを示すブール値です。 **TRUE**の値は、ポートモニターがドライバーに通知を送信することを示します。**FALSE**は、ポートモニターがドライバーに通知を送信しないことを示します。 |
| **filter** | クエリで指定された XML ドキュメントに対して WSD モニターが適用する XPath クエリ。 このトピックの後半の説明を参照してください。 |
| **name** | スキーマ値の名前です。 |
| **query** | WSD モニターが実行するクエリの種類。 |

Microsoft XML (MSXML) 2.6 以降の Windows に実装されている XPath 言語では、XML ファイル内の要素を簡単に指定できます。 詳細については、「 [XPath リファレンス](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256115(v=vs.100))」を参照してください。

`List`コンストラクトは、WsdBidi で定義されています。

## <a name="code-example"></a>コード例

次のコード例では、コンマ区切りのリストが構成されています。この一覧には、"1, 2, 4" のように、N-up 印刷用のシートごとに許容されるページイメージの数が含まれています。

```xml
<Property name='Layout'>
  <Property name='NumberUp'>
    <Property name='PagesPerSheet'>
      <List name='Supported
        query='wprt:PrinterCapabilities'
        filter='wprt:PrinterCapabilites/wprt:JobValues/wprt:DocumentProcessing/wprt:NumberUp/wprt:NUpPagesPerSheet/wprt:AllowedValue'/>
    </Property>
  </Property>
</Property>
```

前の例では、次のクエリが実行されます。

```console
\Printer.Layout.NumberUp.PagesPerSheet:Supported
```
