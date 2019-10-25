---
title: シリアル コントローラー ドライバーの概要
description: Windows のすべてのバージョンで、シリアルコントローラーデバイスのドライバーサポートを提供します。
ms.assetid: 1EA0221E-0F68-429B-9DA5-4AE2D3394A09
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 548be9f69b02f116234f41eb1159605c5a51c9b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845391"
---
# <a name="serial-controller-drivers-overview"></a>シリアル コントローラー ドライバーの概要

Windows のすべてのバージョンで、シリアルコントローラーデバイスのドライバーサポートを提供します。 "*シリアルコントローラー* " という用語は、16550 universal 非同期受信機 (UART) または互換性のあるデバイスを指します。 シリアルコントローラーにはシリアルポートがあり、シリアルポートはシリアルポートを介して、シリアル接続されている周辺機器と通信します。 シリアル通信をサポートするために、Windows には、シリアルの .sys および Serenum.sys ドライバーが含まれています。また、シリアルフレームワーク拡張機能 (SerCx および SerCx2) のバージョン1および2が含まれています。

## <a name="serialsys-and-serenumsys"></a>シリアル .sys と Serenum.sys

Windows 2000 以降、システム提供のシリアルドライバーであるシリアルドライバーは、スタンドアロンのシリアルポート、 [COM ポート](configuration-of-com-ports.md)、およびマルチポートボードをサポートしています。 システム提供のシリアル列挙ドライバーである Serenum.sys は、シリアルポートに接続されているデバイスのうち、Serial .sys または互換性のあるシリアルポートドライバーによって制御されるものを列挙します。 通常、Windows を実行している PC の場合は、通常は COM1 や COM2 などという名前の COM ポートを制御します。 これらのポートは RS-232 標準に緩く準拠していますが、さらに、Pc をサポートするために進化した事実上標準 (電圧レベル、ピン接続、ハードウェアフロー制御など) も組み込まれています。 詳細については、「 [Using Serial .sys And serenum.sys](using-serial-sys-and-serenum-sys.md)」を参照してください。

GitHub の Windows ドライバーサンプルリポジトリには、[シリアル](https://go.microsoft.com/fwlink/p/?LinkId=617962)および[serenum.sys](https://go.microsoft.com/fwlink/p/?LinkId=617961)ドライバーのサンプルのソースコードが含まれています。これらのサンプルは、と同様に動作し、受信トレイのシリアルドライバーと serenum.sys ドライバーの代わりにインストールできます。

## <a name="sercx-and-sercx2"></a>SerCx と SerCx2

Windows 8 以降では、SerCx はシステムによって提供されるコンポーネントで、印刷回路ボードの統合回線間のシリアル通信をサポートしています。 SerCx は、カーネルモードドライバーフレームワーク (KMDF) の拡張機能です。 この拡張機能により、シリアルコントローラー用のカスタムドライバーの開発が簡素化されます。 SerCx は、シリアルコントローラーに共通する多くの処理タスクを処理することによって、拡張機能に基づくシリアルコントローラードライバーを支援します。 このドライバーは、 [sercx デバイスドライバーインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を介して sercx と通信します。

Windows 8.1 以降では、SerCx は SerCx2 によって置き換えられています。 SerCx2 では、シリアルコントローラードライバーのサイズと複雑さを軽減するために、SerCx に対する多くの機能強化が行われています。 特に、SerCx2 はタイムアウトを管理するために必要な処理作業のシリアルコントローラードライバーを解放し、シリアルコントローラーへのアクセスのために競合する i/o トランザクションを調整します。 その結果、シリアルコントローラードライバーが小さく、より単純になります。 シリアルコントローラーのハードウェアベンダーは、シリアルコントローラーのハードウェア固有の機能を管理し、SerCx2 に依存して汎用のシリアルコントローラータスクを実行する、拡張ベースのシリアルコントローラードライバーを提供します。 このドライバーは、 [SerCx2 device driver インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を介して SerCx2 と通信します。

SerCx2 の詳細については、「 [Serial Framework Extension (SerCx2) のバージョン2の使用](using-version-2-of-the-serial-framework-extension.md)」を参照してください。

ドライバーフレームワークに関する一般的な情報については、「 [WDF を使用したドライバーの開発](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="serial-i-o-request-interface.md" data-raw-source="[Serial I/O Request Interface](serial-i-o-request-interface.md)">直列 i/o 要求インターフェイス</a></p></td>
<td><p>シリアルコントローラー上のポートに接続されている周辺機器を制御するために、クライアントアプリケーションまたは周辺機器ドライバーが i/o 要求をポートに送信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="differences-between-sercx2-and-serial-sys.md" data-raw-source="[Differences Between SerCx2.sys and Serial.sys](differences-between-sercx2-and-serial-sys.md)">SerCx2 と http.sys の違い</a></p></td>
<td><p>受信トレイ Sercx2 とシリアルドライバーコンポーネントの両方で<a href="serial-i-o-request-interface.md" data-raw-source="[serial I/O request interface](serial-i-o-request-interface.md)">シリアル i/o 要求インターフェイス</a>が実装されていますが、これらのコンポーネントは交換できません。 これらは、さまざまな要件のセットを満たすように設計されています。</p></td>
</tr>
</tbody>
</table>
