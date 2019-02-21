---
title: AV/C 接続のシナリオ
description: AV/C 接続のシナリオ
ms.assetid: 392f996c-47aa-4ceb-adf9-0c8fd114a511
keywords:
- WDK AV/C の接続
- AV/C WDK、接続のシナリオ
- デジタル ビデオ WDK AV/C
- DV WDK AV/C
- セットトップ ボックス WDK AV/C
- STB WDK AV/C
- テレビの WDK AV/C
- テレビ WDK AV/C
- サブユニット サポート WDK AV/C
- 内通信ユニット接続 WDK AV/C
- WDK AV/C 単位間の接続
- Avc.sys 関数ドライバー WDK、接続
- 外部のプラグイン接続 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c414a77ea2d7d330e62f9cbf383e8ce4adca0914
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537090"
---
# <a name="avc-connection-scenarios"></a>AV/C 接続のシナリオ





Windows Vista では、前に、接続と互換性の管理 (CCM) プロトコルの*Avc.sys*コンピューターが、データ ストリーミングを開始する外部の AV/C デバイスのコント ローラーとして動作する 1 つの接続シナリオでは、サポートされていますデバイスです。 たとえばでの接続管理のストリーミングを開始する*Avc.sys* connect を使用して、デバイス上のサブユニットとデバイス単位のアイソクロナス出力プラグイン間の接続を確立し、単体のコマンド (の切断[**AVC\_関数\_ACQUIRE** ](https://msdn.microsoft.com/library/windows/hardware/ff554148)と[ **AVC\_関数\_リリース**](https://msdn.microsoft.com/library/windows/hardware/ff554169)、それぞれ)。 AV/C 仕様と CCM プロトコルの詳細については、次を参照してください。、 [1394 貿易](https://go.microsoft.com/fwlink/p/?linkid=518448)web サイト。

多くの 7 つの接続シナリオをサポートするために、Windows Vista での接続管理が改善されように*Avc.sys* 8 単位のサブユニット/接続のシナリオをサポートしています。 接続の管理の機能強化のサブユニット プラグから他のサブユニット プラグ; に接続のサポートを追加します。サブユニットは、同じ AV/C 単位内または異なる AV/C 単位で指定できます。 *Avc.sys*信号のソースと入力選択し、CCM プロトコル単位コマンドを使用して接続を確立します。 (*Avc.sys* AV/C 仕様を必要とするレベルにのみ出力プリセットなど他の CCM のプロトコル単位コマンドをサポートしています)。

AV/C ユニットとのサブユニットに関連する接続の 2 つの一般的な種類があります。

-   *ホスト コンピューターとコンピューターに接続する外部デバイスの接続が接続を制御できますが、接続の一部ではない*します。 この接続の種類では、任意のホスト ベースのメモリは使用しません。 代わりに、接続は、デバイスのメモリのないメディアとは、単に、ホストが、コント ローラーとして機能します。 この種類の接続の例は、チューナーのサブユニットのセットトップ ボックス (STB) コンピューターのデータ ストリームを処理せず、デジタルのテレビのモニターのサブユニットに直接データをストリーミングします。

-   *外部デバイスは、標準的なメディアを使用して、ホスト コンピューターに接続し、デバイスから、ホスト コンピューターのメモリにデータをコピーするバッファーを使用して接続*します。 この種類の接続の例では、処理は、後で、コンピューターにデータをストリーミングするデジタル ビデオ (DV) デバイスです。 *Msdv.sys*ドライバーはこの種類の (DV デバイスおよびホスト コンピューター) の間の接続を使用します。

Windows vista の場合に実装されている強化された接続の管理*Avc.sys*接続、デバイスが内部接続するために、AV/C コマンドに応答できますの最初の型に適用されます。 強化された接続の管理*Avc.sys* AV/C CCM プロトコルをサポートして、デバイスの場合との間で異なる AV/C (バス上のデバイスと同じ IEEE 1394)、2 つのテープ サブユニット エンド ツー エンド接続を確立することができます。

**注**  *Avc.sys*接続 (メモリ バッファー) の 2 つ目の種類をサポートしていません。 ただし、接続のメモリ バッファーの種類に依存、 [IEC 61883](https://msdn.microsoft.com/library/windows/hardware/ff537188)プロトコルし、基になるではサポートされて*61883.sys* (、コンピューターに含まれるメモリ バッファーの同じスタック内のドライバー接続の場合)。

 

### <a name="supported-connection-scenarios-in-windows-vista"></a>Windows Vista でサポートされている接続のシナリオ

4 つのシナリオ (1 ~ 4) を表す*内通信*-単位の接続。 これらの接続は、内で完全に 1 つの AV/C の単位に格納されます。 その他の 4 つのシナリオ (5 ~ 8) を表す*inter*-単位の接続。 これらの接続は、2 つの異なる AV/C 単位です。

次のトピックがのメンバーの AV/C 接続管理の 8 つのさまざまなシナリオとそれぞれの値をについて説明します、 [ **AVCCONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554101)構造体。

[サブユニット プラグと 1 つの AV/C 単位内でユニット プラグ間の接続](connections-between-subunit-plugs-and-unit-plugs-within-one-av-c-unit.md)

[1 つの AV/C ユニット内の 2 つのサブユニット プラグ間の接続](connections-between-two-subunit-plugs-within-one-av-c-unit.md)

[2 つのサブユニット プラグ AV/C の異なる単位間の接続](connections-between-two-subunit-plugs-in-different-av-c-units.md)

[異なる AV/C 単位ユニット プラグインするときに 2 つの間の接続](connections-between-two-unit-plugs-in-different-av-c-units.md)

 

 




