---
title: SerCx2 ベースのシリアル コントローラー ドライバーの機能
description: SerCx2 ベースのシリアルコントローラードライバーは kmdf ドライバーで、KMDF のメソッドとコールバックを使用して汎用ドライバー操作を実行し、SerCx2 と通信してシリアルコントローラードライバーに固有の操作を実行します。
ms.assetid: 4A9B80F1-4DE1-4D35-ADDF-90058A4F8388
ms.date: 05/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3246ff757f949cdc0c24a349414dbe21cd09eaf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842444"
---
# <a name="features-of-sercx2-based-serial-controller-drivers"></a>SerCx2 ベースのシリアル コントローラー ドライバーの機能

SerCx2 は、シリアルコントローラードライバーをサポートする特別な機能を備えたカーネルモードドライバーフレームワーク (KMDF) の拡張機能です。 KMDF の詳細については、「 [WDF を使用したドライバーの開発](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)」を参照してください。 SerCx2 ベースのシリアルコントローラードライバーは kmdf のメソッドとコールバックを使用して汎用ドライバー操作を実行し、SerCx2 と通信して実行します。シリアルコントローラードライバーに固有の操作。

通常、シリアルコントローラーは、16550 universal 非同期レシーバー/トランスミッタ (UART) デバイスとのハードウェアレベルで互換性があります。 Uart は、パーソナルコンピューティングの初期時代から、デスクトップ Pc のケースにあるシリアルポートを制御するために使用されてきました。 最近では、serial controller はチップ (SoC) 統合回線上のシステムに含まれています。これにより、他の統合回線との pin の低い通信が提供されます。 SoC ベースのハードウェアプラットフォームでは、クライアントが i/o 要求を送信する "シリアルポート" は、単に SoC チップのシリアルインターフェイスピンのセットになります。 詳細については、「[シリアルコントローラードライバーの概要](serial-drivers-overview.md)」を参照してください。

Microsoft は、同様のハードウェア機能を持つシリアルコントローラーファミリのシリアルコントローラードライバーを提供する場合があります。 または、特別な機能を備えたシリアルコントローラーのハードウェアベンダーが、これらの機能をサポートするためにカスタムシリアルコントローラードライバーを提供する場合があります。

シリアルコントローラードライバーは、デバイスドライバーインターフェイス (DDI) を介して SerCx2 と通信します。 SerCx2 DDI には、次の2つの部分があります。

- SerCx2 によって実装され、シリアルコントローラードライバーによって呼び出されるドライバーサポートメソッドのセット。
- シリアルコントローラードライバーによって実装され、SerCx2 によって呼び出されるイベントコールバック関数のセット。

SerCx2 DDI のメソッドとコールバックの詳細な説明については、 [sercx のヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/)に関するトピックの「バージョン 2 Serial Framework Extension (SerCx2) Reference」を参照してください。

ハードウェアベンダーには、スタンドアロンのシリアルコントローラードライバーを作成するオプションがありますが、それには大きな労力が必要です。 これに対して、SerCx2 を使用するシリアルコントローラードライバーを開発する方が簡単です。通常、ドライバーははるかに小さく、信頼性が高くなります。

SerCx2 は、コントローラードライバーに代わって次のタスクを管理します。

- 読み取りおよび書き込み操作
- 直列 i/o タイムアウト検出
- ハードウェアイベント
- システム DMA 転送 (システム DMA トランザクションがサポートされている場合)
- 低電力デバイスの状態との間の切り替え
- I/o 要求のキャンセル (カスタム i/o トランザクション中を除く)

SerCx2 は、読み取りと書き込みの操作を管理するために、 [**irp\_MJ\_read**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))および[**irp\_MJ\_書き込み**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))要求を、シリアルコントローラードライバーが処理するために比較的単純な i/o トランザクションに変換します。 詳細については、「 [SerCx2 i/o](sercx2-i-o-transactions.md)transaction」を参照してください。

SerCx2 は、Sercx2 という名前のコンポーネントとして Windows に含まれています。 シリアルコントローラードライバーは、SerCx2 ライブラリ (バージョン 2.0) に静的にリンクされ、実行時に Sercx2 と通信します。 SerCx2 DDI は、2.0\\Sercx .h のヘッダーファイルで定義されています。 Windows Driver Kit for Windows 8.1 では、sercxstubs .lib と Sercx. h を利用できます。
