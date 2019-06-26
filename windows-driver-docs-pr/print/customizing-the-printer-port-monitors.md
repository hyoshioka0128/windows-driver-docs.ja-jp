---
title: プリンター ポート モニターをカスタマイズする
description: プリンター ポート モニターをカスタマイズする
ms.assetid: e5d4166a-2593-43fd-b476-c54642e2d099
keywords:
- 組み込みの自動構成サポート WDK プリンター、プリンター ポート モニターをカスタマイズします。
- 双方向の拡張機能は、WDK プリンター autoconfig をファイルします。
- ボックスの自動構成サポートの WDK プリンター、双方向の拡張ファイル
- WDK を監視するプリンター ポートをカスタマイズします。
- WDK のポート モニターが印刷をカスタマイズします。
- 双方向のデータへの変換を WinSNMP WDK プリンターを入力します。
- 双方向通信 WDK の印刷
- 双方向通信 WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36f4eba5f7f96da40ca254e07ca518359fcc53b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372370"
---
# <a name="customizing-the-printer-port-monitors"></a>プリンター ポート モニターをカスタマイズする


標準を上回る機能を備えた印刷デバイス用の新しいスキーマを定義する[双方向通信スキーマ](bidirectional-communication-schema.md)標準 TCP/IP またはに付属している Devices (WSD) ポート モニター用の Web サービスをカスタマイズします。Windows Vista の場合。 双方向の拡張ファイル、ドライバーを特定の新しいスキーマを定義する XML ファイルを作成する必要があります。 ドライバーがインストールされている場合、この拡張機能ファイルがインストールされます。 TCP/IP または WSD ポート モニターは、この拡張機能ファイルを識別する、モニターは、ファイルを読み込みし、追加 bidi スキーマを使用できます。

双方向の拡張ファイル内のスキーマは、標準の印刷スキーマのサブセットです。 このようなスキーマは、WDK で提供される Tcpbidi.xsd または WsdBidi.xsd ファイルの構造に従う必要があります。

**注**  場合、[双方向通信のスキーマ](bidirectional-communication-schema.md)要件に、双方向の拡張機能ファイルを作成し、印刷ポート モニターをカスタマイズする必要があるためありません必要はありません。

 

双方向の拡張機能ファイルを作成し、次の条件のいずれかが当てはまる場合にプリンタ ドライバに関連付ける必要があります。

1.  プリンター ドライバーには、標準の印刷スキーマに見つかりませんのプリンター情報が必要があります。 この情報を取得するには、追加のクエリでサポートされているスキーマを拡張する必要があります。 特定のポートに対してサポートされているスキーマを列挙するその他のクライアントは、追加のクエリを取得しますが、通常は理解できません。

2.  標準の TCP/IP のサポートされていない標準の印刷スキーマからのクエリを追加する予定または WSD ポートは、クエリには、ドライバー固有の情報が必要があるために、監視します。 この場合、印刷スキーマを拡張する必要があります。 通常、入力と出力に関連する印刷スキーマの部分を拡張する必要が印刷メディアのビン。 ビン bidi スキーマとプリンターの管理情報ベース (MIB) で定義されているため、名前の間のマッピングを提供することも必要があります。

3.  など、カスタム オブジェクト識別子 (OID) を設定したり、更新間隔を変更する方法の標準のクエリの作業をカスタマイズする予定があります。 たとえば、標準の TCP/IP ポート モニタは、600 秒 (10 分) の既定の間隔で Web サービスのイベント処理をサポートしていないデバイスをポーリングします。 RefreshInterval 属性を設定する双方向の拡張機能を作成してポーリング間隔を変更することができます、[値](value.md)デバイスに関連付けられている構造。 (を参照してください、`Memory`プロパティに次のコード例です)。

標準印刷スキーマで双方向通信のサポートがドライバーに固有のデータを必要とするクエリに応答できない関連付けられた双方向の拡張ファイル、ドライバーがない場合は、(データに関連するなど、入力と出力のビン)。

**注**   Windows Vista でのルーティングのコンパートメントが適切に信頼されたプロセスが別のネットワークに接続を許可するネットワーク インターフェイス (仮想または物理) かどうかを互いから分離されたさまざまなインターフェイスを維持しながらします。 たとえば、Windows Vista では、VPN とユーザーのローカル ネットワークとインターネットの両方に同時にアクセスできないようにする VPN ポリシーを適用するのにこれらのコンパートメントを使用します。 印刷時に、スプーラーは、TCP のプリンター ポートを開くときに、ユーザーを偽装します。 その結果、スプーラーは、ユーザーが VPN に接続されているローカル ネットワーク プリンターに印刷できません。

 

### <a name="structure-of-a-bidi-extension-file"></a>双方向の拡張機能ファイルの構造

双方向の拡張機能ファイルが正しく構成されている XML を Microsoft Windows Driver Kit (WDK) で指定された Tcpbidi.xsd または WsdBidi.xsd ファイルを無効にする必要があります。 これらの .xsd ファイルで定義された構成要素には、新しいスキーマを定義することが有効にします。

次は、その基本的な構造を表示する TCP/IP bidi 拡張ファイルの不完全な例です。 WSD 双方向の拡張機能ファイルの構造は似ています。

```cpp
<?xml version="1.0" encoding="US-ASCII"?>
<bidi:Schema xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
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

上記のコード例に注意してください。

-   ルート要素には、ただ 1 つのスキーマ要素が含まれています。 スキーマの階層は、スキーマの要素で始まります。

-   スキーマ要素には、プロパティ要素がノードと値の要素になりますがあります。

-   値の各要素は、データを取得できる特定の手法を定義します。

### <a name="conversion-of-winsnmp-to-bidi-data-types"></a>WinSNMP 双方向のデータ型への変換

簡易ネットワーク管理プロトコル (SNMP) の種類と bidi 型間の通信がで指定された、 [ **BIDI\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type)列挙トピック。

このセクションの残りの部分には、独自の bidi スキーマの拡張機能を作成するために、次のトピックが含まれています。

[TCP/IP のスキーマの拡張機能](tcp-ip-schema-extensions.md)

[WSD スキーマの拡張機能](wsd-schema-extensions-for-driver-specific-queries.md)

 

 




