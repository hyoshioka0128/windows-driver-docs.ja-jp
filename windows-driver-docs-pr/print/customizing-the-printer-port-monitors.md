---
title: プリンター ポート モニターをカスタマイズする
description: プリンター ポート モニターをカスタマイズする
ms.assetid: e5d4166a-2593-43fd-b476-c54642e2d099
keywords:
- 組み込みの自動構成サポート WDK プリンター、プリンターポートモニターのカスタマイズ
- bidi 拡張ファイル WDK プリンター autoconfig
- 組み込み自動構成サポート WDK プリンター、bidi 拡張ファイル
- プリンタポートモニタのカスタマイズ (WDK)
- ポートモニター WDK 印刷、カスタマイズ
- WinSNMP データ型の WDK プリンタへの変換
- 双方向通信の WDK 印刷
- bidi 通信 WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96107191274be66401a1d94355d0aa97472e002
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652818"
---
# <a name="customizing-the-printer-port-monitors"></a>プリンター ポート モニターをカスタマイズする


Windows Vista に付属している標準 TCP/IP または Web Services for Devices (WSD) ポートモニタをカスタマイズすることによって、標準の[bidi 通信スキーマ](bidirectional-communication-schema.md)以上の機能を持つ印刷デバイスの新しいスキーマを定義できます。 Bidi 拡張ファイルを作成する必要があります。これは、そのドライバーに固有の新しいスキーマを定義する XML ファイルです。 この拡張ファイルは、ドライバーのインストール時にインストールされます。 TCP/IP または WSD ポートモニターがこの拡張ファイルを識別すると、モニターによってファイルが読み込まれ、追加の bidi スキーマを使用できるようになります。

Bidi 拡張ファイルのスキーマは、標準の印刷スキーマのサブセットです。 このようなスキーマは、WDK で提供される Tcpbidi .xsd ファイルまたは WsdBidi ファイルの構造に従う必要があります。

**注**  [bidi 通信スキーマ](bidirectional-communication-schema.md)が要件を満たしている場合は、bidi 拡張ファイルを作成する必要はないため、印刷ポートモニターをカスタマイズする必要はありません。

 

次の条件のいずれかに該当する場合は、bidi 拡張ファイルを作成し、プリンタードライバーに関連付ける必要があります。

1.  プリンタードライバーは、標準の印刷スキーマでは見つからないプリンターの情報を必要とします。 この情報を取得するには、追加のクエリを使用して、サポートされているスキーマを拡張する必要があります。 特定のポートでサポートされているスキーマを列挙するその他のクライアントは、追加のクエリを取得しますが、通常はそれを理解できません。

2.  標準の TCP/IP または WSD ポートモニターでサポートされていない標準の印刷スキーマからのクエリを含めることを計画しています。これは、クエリにドライバー固有の情報が必要なためです。 この場合、印刷スキーマを拡張する必要があります。 通常は、印刷メディアの入力ビンと出力ビンに関連する印刷スキーマの部分を拡張する必要があります。 また、bidi スキーマで定義されているビンの名前と、プリンターの管理情報ベース (MIB) のビン名の間のマッピングも指定する必要があります。

3.  カスタムオブジェクト識別子 (OID) を設定したり、更新間隔を変更したりするなど、標準クエリの動作方法をカスタマイズします。 たとえば、標準 TCP/IP ポートモニターは、Web サービスイベントをサポートしていないデバイスを、既定の600秒 (10 分) でポーリングします。 ポーリング間隔を変更するには、デバイスに関連付けられている[値](value.md)コンストラクトで refreshInterval 属性を設定する bidi 拡張機能を作成します。 (次のコード例では、`Memory` プロパティを参照してください)。

ドライバーに関連付けられた bidi 拡張ファイルがない場合、標準の印刷スキーマでの bidi 通信のサポートは、ドライバー固有のデータ (入力ビンと出力ビンに関連するデータなど) を必要とするクエリに応答できません。

**注**   Windows Vista のネットワークルーティングコンパートメントを使用すると、信頼できるプロセスによって、さまざまなインターフェイスが相互に分離された状態で、さまざまなネットワークインターフェイス (仮想または物理) に接続できます。 たとえば、Windows Vista は、これらのコンパートメントを使用して、VPN とユーザーのローカルネットワークとインターネットの両方への同時アクセスを許可しない VPN ポリシーを適用します。 印刷中は、TCP プリンターポートを開くときにスプーラによってユーザーの権限が借用されます。 このため、ユーザーが VPN に接続している間、スプーラはローカルネットワークプリンターに出力できません。

 

### <a name="structure-of-a-bidi-extension-file"></a>Bidi 拡張ファイルの構造

Bidi 拡張ファイルは、Microsoft Windows Driver Kit (WDK) に用意されている Tcpbidi .xsd ファイルまたは WsdBidi ファイルに従って有効である必要がある、整形式の XML です。 これらの .xsd ファイルで定義されているコンストラクトを使用して、新しいスキーマを定義できます。

次に示すのは、基本的な構造を示す TCP/IP bidi 拡張ファイルの完全な例です。 WSD bidi 拡張ファイルの構造は似ています。

```cpp
<?xml version="1.0" encoding="US-ASCII"?>
<bidi:Schema xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Schema>
    <Property name="Printer">
      <Property name="Configuration">
        <Property name= "Memory">
          <Value name="Size" type="BIDI_INT" oid="1.3.6.1.2.1.25.2.2" refreshInterval="600" drvPrinterEvent="true" />
          .
          .
          .
        </Property>
      </Property>
    </Property>
  </Schema>
</bidi:Schema>
```

前のコード例では、次の点に注意してください。

-   ルート要素には、スキーマ要素が1つだけ含まれます。 スキーマの階層は、スキーマ要素で始まります。

-   Schema 要素には、ノードとしてのプロパティ要素とリーフとしての値要素があります。

-   各値要素は、データを取得するための特定の手法を定義します。

### <a name="conversion-of-winsnmp-to-bidi-data-types"></a>WinSNMP から Bidi データ型への変換

Simple Network Management Protocol (SNMP) 型と bidi 型の対応については、「 [**bidi\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)列挙型」を参照してください。

このセクションの残りの部分では、独自の bidi スキーマ拡張を作成する際に役立つ次のトピックについて説明します。

[TCP/IP スキーマ拡張](tcp-ip-schema-extensions.md)

[WSD スキーマ拡張](wsd-schema-extensions-for-driver-specific-queries.md)

 

 




