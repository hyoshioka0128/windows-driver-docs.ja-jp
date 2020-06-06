---
title: Installed (WSD)
description: Web Services for Devices (WSD) Installed コンストラクトは、特定の条件セットに一致するプリンター機能がインストールされているかどうかを示します。
ms.assetid: f05add2a-d37e-4eb5-8408-dd5eeef4b13c
keywords:
- インストールされたコンストラクト
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 369682a4c24438b204309d86916cf98262f9062d
ms.sourcegitcommit: 581fb777a2376854ca12e767d366e2cb79724b73
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84461831"
---
# <a name="installed-wsd"></a>Installed (WSD)

Web Services for Devices (WSD) Installed コンストラクトは、特定の条件セットに一致するプリンター機能がインストールされているかどうかを示します。 XPath フィルターが、指定された条件に適用されるときに有効な XML 結果を取得する場合、このアルゴリズムは**TRUE**を返します。 インストールされているコンストラクトは、WsdBidi で定義されています。

| 属性 | 説明 |
| --- | --- |
| **drvPrinterEvent** | Optionalポートモニターがドライバーに通知を送信するかどうかを示すブール値です。 **TRUE**の値は、ポートモニターがドライバーに通知を送信することを示します。**FALSE**は、ポートモニターがドライバーに通知を送信しないことを示します。 |
| **filter** | クエリで指定された XML ドキュメントに対して WSD モニターが適用する XPath クエリ。 このトピックの後半の説明を参照してください。 |
| **name** | スキーマ値の名前です。 |
| **query** | WSD モニターが実行するクエリの種類。 |

Microsoft XML (MSXML) 2.6 以降の Windows に実装されている XPath 言語では、XML ファイル内の要素を簡単に指定できます。 詳細については、「 [XPath リファレンス](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256115(v=vs.100))」を参照してください。

インストールされた構成要素の動作は、その親ノードの定義によって異なります。 インストールされているコンストラクトがパラメーターを使用せずに指定されている場合は、クエリの実行時に常にスキーマが存在します。 インストールされているコンストラクトがパラメーターを使用して指定されている場合、関連付けられているパラメーター値が現在の WSD デバイスクエリで見つかった場合にのみ、スキーマが存在します。 クエリを実行するソフトウェアは、インストールされているスキーマが返されないケースを処理できる必要があります。

インストールされているコンストラクトは、WsdBidi で定義されています。

## <a name="code-example"></a>コード例

次のコード例では、フィルター検索アルゴリズムで XPath クエリを使用して、ハードディスクがインストールされていることを確認します。

```xml
<Schema>
  <Property name='Printer'>
    <Property name='Configuration'>
      <Property name='HardDisk'>
        <Installed name='Installed'
            query='wprt:PrinterConfiguration'
            filter='wprt:PrinterConfiguration/wprt:Storage/wprt:StorageEntry[wprt:Type="HardDisk"]'/>
      </Property>
    </Property>
  </Property>
</Schema>
```

前の例では、次のクエリが実行されます。

```cpp
\Printer.Configuration.HardDisk:Installed
```
