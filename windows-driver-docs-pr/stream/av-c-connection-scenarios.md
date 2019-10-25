---
title: AV/C 接続シナリオ
description: AV/C 接続シナリオ
ms.assetid: 392f996c-47aa-4ceb-adf9-0c8fd114a511
keywords:
- 接続 WDK AV/C
- AV/C WDK、接続シナリオ
- デジタルビデオ WDK AV/C
- DV WDK AV/C
- セットトップボックス WDK AV/C
- STB WDK AV/C
- TV WDK AV/C
- テレビ WDK AV/C
- サブユニットは WDK AV/C をサポートします
- ユニット内接続の WDK AV/C
- ユニット間接続の WDK AV/C
- Avc 関数ドライバー WDK、接続
- 外部プラグ接続 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c62ae8ec252385b330f9479551e47a5cec9ee68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843365"
---
# <a name="avc-connection-scenarios"></a>AV/C 接続シナリオ





Windows Vista より前の場合、 *Avc*の接続と互換性管理 (CCM) プロトコルでは単一の接続シナリオがサポートされています。このシナリオでは、外部の AV/C デバイスがデバイスからデータストリーミングを開始するためのコントローラーとして機能していました。 たとえば、ストリーミングを開始するには、デバイスのサブユニットとデバイスユニットのアイソクロナス出力プラグの間の接続を確立するために、接続と切断ユニットのコマンド (Avc\_を使用し*ます。* [**関数\_取得**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-acquire)と[**AVC\_関数\_リリース**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-release))。 AV/C 仕様と CCM プロトコルの詳細については、1394の[取引アソシエーション](https://go.microsoft.com/fwlink/p/?linkid=518448)web サイトを参照してください。

Windows Vista では、7つ以上の接続シナリオをサポートするために接続管理が強化されているため、 *Avc*は8つのユニット/サブユニット接続シナリオをサポートします。 接続管理の機能強化により、サブユニットプラグから他のサブユニットプラグへの接続のサポートが追加されました。サブユニットは、同じ AV/C ユニット内、または別の AV/C ユニットに配置できます。 *Avc*は、signal source を使用して接続を確立し、次に CCM プロトコルユニットコマンドを入力します。 (*Avc. sys*では、出力プリセットなどの他の CCM プロトコルユニットコマンドがサポートされているのは、AV/C 仕様で必要なレベルのみです)。

AV/C ユニットとサブユニットに関連する一般的な接続には、次の2種類があります。

-   *外部デバイスがホストコンピューターに接続し、コンピューターが接続を制御できるが接続の一部ではない接続*。 この接続の種類では、ホストベースのメモリは使用されません。 この接続は、デバイスを含むメモリ不足メディアであり、ホストは単にコントローラーとして機能します。 この種類の接続の例として、データストリームを処理するコンピューターを使用せずに、デジタルテレビの監視サブユニットにデータを直接ストリーミングするセットトップボックス (STB) のチューナーサブ区分があります。

-   *外部デバイスが標準メディアを使用してホストコンピューターに接続し、バッファーを使用してデバイスからホストコンピューターのメモリにデータをコピーする接続*。 この種類の接続の例として、デジタルビデオ (DV) デバイスがあります。このデバイスでは、データをコンピューターにストリーミングし、後で処理します。 *Msdv .sys*ドライバーは、この種類の接続 (DV デバイスとホストコンピューターの間) を使用します。

*Avc*で Windows Vista に実装される強化された接続管理は、最初の種類の接続に適用されます。この場合、デバイスは AV/C コマンドに応答して内部接続を行うことができます。 *Avc*での接続管理の強化により、デバイスが Av/c CCM プロトコルをサポートしている場合、異なる Av/c デバイス (同じ IEEE 1394 バス) にある2つのテープサブユニット間のエンドツーエンド接続を確立できます。

**注**  *Avc*は、2番目の種類の接続 (メモリバッファー) をサポートしていません。 ただし、接続のメモリバッファーの種類は、 [IEC 61883](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-client-drivers)プロトコルに従い、基になる*61883 .sys*ドライバーが同じスタック (コンピューターがメモリバッファー接続に関係する場所) でサポートされています。

 

### <a name="supported-connection-scenarios-in-windows-vista"></a>Windows Vista でサポートされている接続シナリオ

4つのシナリオ (1 ~ 4) は、ユニット*内*接続を表します。 これらの接続は、1つの AV/C ユニット内に完全に含まれています。 他の4つのシナリオ (5 ~ 8) は、ユニット*間*の接続を表します。 これらの接続は、2つの異なる AV/C ユニット間にあります。

次のトピックでは、8つの異なる AV/C 接続管理シナリオと、 [**Avcconnectinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)構造体のメンバーに対応する値について説明します。

[1つの AV/C ユニット内のサブユニットプラグとユニットプラグ間の接続](connections-between-subunit-plugs-and-unit-plugs-within-one-av-c-unit.md)

[1つの AV/C ユニット内の2つのサブユニット間の接続](connections-between-two-subunit-plugs-within-one-av-c-unit.md)

[2つのサブユニットが異なる AV/C ユニットに接続する](connections-between-two-subunit-plugs-in-different-av-c-units.md)

[異なる AV/C ユニットにある2つのユニットプラグ間の接続](connections-between-two-unit-plugs-in-different-av-c-units.md)

 

 




