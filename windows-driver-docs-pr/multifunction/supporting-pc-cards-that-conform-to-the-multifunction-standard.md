---
title: 多機能標準に準拠した PC カードのサポート
description: 多機能標準に準拠した PC カードのサポート
ms.assetid: 1ab295b6-42c9-46fc-97e0-2228e189ff37
keywords:
- PCMCIA バス WDK 多機能デバイス
- mf.inf
- ハードウェア Id の WDK 多機能デバイス
- 子関数のハードウェア Id の WDK 多機能デバイス
- システム提供の多機能バス ドライバー WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb53e8bceeb05b58c0bd6c9e901cfd414ea4aa0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581077"
---
# <a name="supporting-pc-cards-that-conform-to-the-multifunction-standard"></a>多機能標準に準拠した PC カードのサポート





ISA スタイル PC カード デバイス、PC カード多機能標準を完全に実装する場合は 16 ビット NT ベースのプラットフォーム上のようなデバイスのベンダーだけを使用正しくのソフトウェアの側面を処理するために次のシステムが指定したコンポーネントにし、多機能セマンティクスは:

-   多機能デバイスの INF ファイル。 (システム提供の)

    PCMCIA バス ドライバーには、システム提供多機能 INF ファイル (mf.inf) を使用してデバイスを構成する、configuration manager を原因となるデバイスのハードウェア ID を指定します。 Mf.inf ファイルでは、(devguid.h で定義) された「多機能」クラスとその GUID を指定します。

-   多機能デバイス関数ドライバー。 (システム提供の)

    Mf.inf ファイルでは、デバイスの機能のドライバーとしてシステム提供の多機能バス ドライバー (mf.sys) を指定します。

    Mf.sys バス ドライバーでは、デバイスの機能を列挙します。 PCMCIA バス ドライバーでは、各関数のリソース要件を決定するデバイスの構成のレジスタを読み取ります。

    参照してください[System-Supplied 多機能バス ドライバーを使用して](using-the-system-supplied-multifunction-bus-driver.md)詳細については、システム提供の mf.sys ドライバーを使用します。

多機能標準に準拠している PC カード デバイスのベンダーでは、個々 の関数の次のサポートを提供する必要があります。

-   デバイスの各関数の関数の PnP ドライバー。 (ベンダーから提供された)

    多機能バス ドライバーでは、多機能のセマンティクスを処理するため、関数のドライバーは、関数は、個々 のデバイスとしてパッケージ化された場合に使用される同じドライバーを指定できます。

-   各関数の場合、デバイスの INF ファイル。 (ベンダーから提供された)

    INF ファイルには、関数は、個々 のデバイスとしてパッケージ化された場合に使用される同じファイルを指定できます。 INF ファイルでは、多機能の特殊なセマンティクスは必要ありません。

### <a name="child-function-hardware-ids-created-by-the-pcmcia-bus-driver"></a>PCMCIA バス ドライバーによって作成された子関数のハードウェア Id

PC カード デバイスでは true、多機能の PCMCIA バス ドライバーの mf.sys、と共には子関数のハードウェア Id を作成します。 これらの Id ではの形式があります。

```cpp
    <Manufacturer-name>-<Product-ID-string>-DEV<number>-CRC
```

この形式で&lt;*数*&gt;関数の 0 から始まる番号です。

たとえば、PCMCIA バス ドライバーでは子関数に、次のハードウェア Id が作成されます。

```cpp
    3COM_Corporation-3C562D/3C563D-DEV0-4893
    3COM_Corporation-3C562D/3C563D-DEV1-4893
```

子関数の多機能 PC カード デバイスの INF ファイルを mf.sys、PCMCIA バス ドライバーによって報告されるハードウェア ID を指定する必要があります。

 

 




