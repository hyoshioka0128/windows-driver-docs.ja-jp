---
title: SerCx2 ベースのシリアル コントローラー ドライバーの機能
description: シリアル コント ローラーの SerCx2 ベースのドライバーは、KMDF に汎用ドライバー操作を実行するメソッドとコールバックを使用して、コント ローラーのシリアル ドライバーに固有の操作を実行する SerCx2 と通信する KMDF ドライバーです。
ms.assetid: 4A9B80F1-4DE1-4D35-ADDF-90058A4F8388
ms.date: 05/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6759434255ae8cf496d670bbcda6fff99d38d6d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377925"
---
# <a name="features-of-sercx2-based-serial-controller-drivers"></a>SerCx2 ベースのシリアル コントローラー ドライバーの機能

SerCx2 は、シリアル コント ローラーのドライバーをサポートするために特別な機能を持つカーネル モード ドライバー フレームワーク (KMDF) に拡張機能です。 詳細については、KMDF」を参照して[ドライバーの開発に WDF を使用して](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)A SerCx2 ベース シリアル コント ローラーのドライバーは、KMDF ドライバー KMDF に汎用ドライバー操作を実行するメソッドとコールバックを使用して、通信します。SerCx2 シリアル コント ローラーのドライバーに固有の操作を実行します。

通常、シリアル コント ローラーが互換性のあるハードウェア レベルで 16550 ユニバーサル非同期受信側/送信元 (UART) デバイスを使用します。 コントロールをパーソナル コンピューティングの時代シリアル ポートは、デスクトップ Pc の場合は、上にあるので、Uart を使用されています。 最近では、シリアル コント ローラーは、その他の統合の回線でピン数の少ない通信を提供するチップ (SoC) 統合の回線でシステムに格納されます。 SoC ベースのハードウェア プラットフォームでは、クライアントが I/O 要求を送信する「シリアル ポート」は、SoC チップのピン シリアル インターフェイスのセットですが。 詳細については、次を参照してください。[シリアル コント ローラーのドライバーの概要](serial-drivers-overview.md)します。

Microsoft では、同様のハードウェア機能があるシリアルのコント ローラーのファミリ用シリアル コント ローラー ドライバーを提供可能性があります。 または、これらの機能をサポートするためにカスタムのシリアル コント ローラーのドライバーを提供する特別な機能を備えたシリアル コント ローラーのハードウェアの製造元。

シリアル コント ローラー ドライバーは、デバイス ドライバー インターフェイス (DDI) を通じて SerCx2 と通信します。 SerCx2 DDI では、2 つの部分があります。

- シリアル コント ローラー ドライバーによっては、一連の SerCx2 によって実装されているドライバー サポート メソッドが呼び出されます。
- シリアル コント ローラー ドライバーによって実装され、SerCx2 によって呼び出されるイベント コールバック関数のセット。

メソッドと SerCx2 DDI でコールバックの詳細については、バージョン 2 シリアル フレームワーク拡張 (SerCx2) リファレンスを参照してください、 [sercx.h ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/)トピック。

ハードウェア ベンダーには、スタンドアロン シリアル コント ローラーのドライバーを作成するオプションがありますが、そのためには多大な労力が必要です。 比較すると、SerCx2 を使用するコント ローラーのシリアル ドライバーの開発が簡単と、はるかに小さいより信頼性の高いドライバー通常発生します。

SerCx2 では、コント ローラーのドライバーの代わりに、次のタスクを管理します。

- 読み取りおよび書き込み操作
- シリアル I/O タイムアウトの検出
- ハードウェア イベント
- システム DMA (システム DMA のトランザクションがサポートされている) 場合の転送します。
- 低電力デバイスの状態との間の遷移
- I/O 要求のキャンセル (カスタム I/O トランザクション中を除く)

SerCx2 の変換を読み取りを管理し、書き込み操作、 [ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))と[ **IRP\_MJ\_書き込み** ](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))を処理するコント ローラーのシリアル ドライバーの比較的単純な I/O トランザクションをクライアントからの要求。 詳細については、次を参照してください。 [SerCx2 I/O トランザクション](sercx2-i-o-transactions.md)です。

SerCx2 は、Sercx2.sys という名前のコンポーネントとして Windows に含まれます。 シリアル コント ローラー ドライバー静的 Sercxstubs.lib (バージョン 2.0) である SerCx2 ライブラリへのリンクし、実行時に、通信 Sercx2.sys します。 SerCx2 DDI が 2.0 に定義されている\\Sercx.h ヘッダー ファイル。 Windows 8.1 の Windows ドライバー キットで使用できる Sercxstubs.lib と Sercx.h します。
