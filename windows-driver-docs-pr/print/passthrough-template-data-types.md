---
title: パススルー テンプレート データ型
description: パススルー テンプレート データ型
ms.assetid: 9e5e6a12-5847-45fe-bee5-68944cd546d7
keywords:
- WDK GDL、データ型のテンプレート
- WDK GDL、プリミティブのデータ型
- パススルーのデータ型の WDK GDL
- スキーマ WDK GDL、パススルーのデータ型の検証
- ArrayLabel ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 603633367691a26812f00800d17d7960169feb05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380686"
---
# <a name="passthrough-template-data-types"></a>パススルー テンプレート データ型


\***DataType**:**パススルー**未処理のデータ型を表すテンプレートを定義します。 GDL 属性を表す XML 要素の要素のコンテンツとして GDL 値を構成する文字が挿入されます。

次のディレクティブは、パススルーのデータ型を定義するテンプレート内で認識されます。

-   \*ArrayLabel します。 このディレクティブが指定されている場合、パーサー フィルターがで値をかっこで囲む必要があり、前に、指定した配列のラベル。 このディレクティブは省略可能です。

値の構文は、文字データや、子要素を含む XML 要素のコンテンツに対して定義されている構文に準拠する必要があります。 開始タグまたは右角かっこのような文字が GDL パーサーは特殊な XML をエスケープしないことに注意してください (&lt;または&gt;) またはアンパサンド (&)。 値の作成者は、要素の内容の XML 構文を値に準拠します。

全体の値 (または競合している部分のみ) で囲む必要があります XML 構文は、基本的な GDL 構文規則と競合している場合&lt;Begin/EndValue:&gt;を構築します。 このような互換性のない構文では、使用した XML 値または構文は、複合データ型で使用される構文と互換性がない、複合データ型のメンバーとして表示されることはできませんが、GDL 属性の値として直接表示する必要があります。

たとえば、次のテンプレートの例を検討してください。

```cpp
*Template:  ELEMENT_CONTENT
{
    *Type:  DATATYPE
    *DataType:   PASSTHROUGH
}
```

上記のテンプレートを使用して、パーサー フィルターは、パススルー データの XSD スキーマのデータ型の宣言を作成できません。

次の GDL エントリを検討してください。

```cpp
*InLineXML:  <BeginValue:XML>
 <Cell CellOrdinal="0">
         <Value xsi:type="xsd:double">16890</Value>
         <FmtValue>16,890.00</FmtValue>
         <FormatString>Standard</FormatString>
      </Cell>
<EndValue:XML>
```

前の例のテンプレートを使用して、上記のエントリを解釈する場合は、次の XML 出力が発生します。

```cpp
<GDL_ATTRIBUTE Name="*InLineXML"  >
  <Cell CellOrdinal="0">
    <Value xsi:type="xsd:double">16890</Value>
    <FmtValue>16,890.00</FmtValue>
    <FormatString>Standard</FormatString>
  </Cell>
</GDL_ATTRIBUTE>
```

使用する必要があります XML スキーマを使用してパススルー インスタンスを検証する場合、 [XSD\_定義データ型](xsd-template-data-types.md)パススルーではなくため、XSD\_定義データ型を XSD スキーマを使用します。明示的にテンプレートで定義されているし、は、パーサーでスキーマの出力に統合されています。

 

 




