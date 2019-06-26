---
title: プリンター ドライバー アーキテクチャ
description: プリンター ドライバー アーキテクチャ
ms.assetid: 68a61007-8f0d-4fd4-b4a7-c8acbc101236
keywords:
- 印刷ジョブ WDK、プリンター ドライバー
- WDK のジョブの印刷、プリンター ドライバー
- Windows 印刷アーキテクチャ WDK
- プリンター ドライバーのアーキテクチャ WDK
- プリンター ドライバー WDK、アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8475113b5d684cf49f09b7effbcddd96522dece
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380633"
---
# <a name="printer-driver-architecture"></a>プリンター ドライバー アーキテクチャ





Microsoft Win32 GDI または Windows vista、Windows Presentation Foundation (WPF) 関数の呼び出しを通じて、アプリケーションから印刷ジョブが作成されます。 Win32 関数は、EMF、としてアプリケーション データをスプールまたはすぐに各ドキュメントのページの印刷可能なイメージをレンダリングすることができます。 WPF は、スプールのアプリケーション データを XPS スプール ファイルとして機能します。

Windows Vista では、前にアプリケーションを使用して、プリンターのプリンター設定を伝え、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体。 Windows Vista では、印刷チケットと印刷機能のテクノロジは、プリンターやアプリケーション全体でプリンターの設定がより互換性のあるようににプリンターの設定を通信します。

画像レンダリング、すぐに、または印刷の処理中に実行するかどうかは、印刷ドライバーで実行されます。

-   A [GDI ベースのプリンター ドライバー](gdi-printer-drivers.md)スプール ファイルから EMF レコードの再生中にイメージのレンダリングを実行し、GDI レンダリング エンジンによって制御されます。 レンダリング操作中には、GDI レンダリング エンジンは、アシスタンスの適切な Windows 2000 と以降のバージョンのプリンター ドライバーを呼び出します。

-   [XPSDrv プリンター ドライバー](xpsdrv-printer-drivers.md) XPS スプール ファイルの内容をプリンターに出力を処理する一連のフィルター処理を使用します。

Windows 2000 および後で GDI ベースのプリンター ドライバーが必要です。

-   GDI をサポートできない提供のプリンター固有の描画機能によって、レンダリングの印刷ジョブで GDI を支援します。

-   印刷スプーラーに描画された画像のデータ ストリームを送信します。

-   関連付けられたプリンターおよび印刷するドキュメント、どの入力と出力としてトレイが選択されているようなコピー、画像の解像度と印刷の向きの数と変更可能な構成パラメーターにユーザー インターフェイスを提供します。

XPSDrv プリンター ドライバーでは、GDI ベースのドライバーと同じユーザー インターフェイス責任があるし、も、印刷ジョブ データの処理とデータをプリンターに送信する責任を負います。 XPSDrv プリンター ドライバーは、ただし、GDI を使用して、プリンターのページのイメージをレンダリングするには必要ありません。

Windows 2000 とプリンター ドライバーを後で構成される、一連の[プリンター ドライバー コンポーネント](gdi-printer-drivers.md)個別の Dll にドライバーを描画し、ユーザー インターフェイスの操作を分割します。 XPSDrv プリンター ドライバーは、分割、構成設定、描画、および個々 のオブジェクトに関数を表示するコンポーネントの構成もされます。

このセクションでは、Windows 2000 と以降のオペレーティング システムがサポートするプリンター ドライバーのさまざまな種類の理解に役立つものですが、次の 3 つのプリンター ドライバーはオペレーティング システムに付属することも覚えて必要があります。

[Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md)

[Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md)

[Microsoft プロッター ドライバー](microsoft-plotter-driver.md)

これら 3 つのドライバーでは、エンドユーザーが今すぐ購入できるほとんどの印刷デバイスをサポートします。 印刷デバイスが適切な Microsoft 提供のドライバーと互換性がないかどうか、プリンター ドライバーのみを記述する必要があります。 追加するだけでほとんどの新しいプリンターをサポートすることができます、[データ ファイルをプリンター](printer-data-files.md) Microsoft 提供のドライバーのいずれかにします。 新しいドライバーが必要となるデバイスには、これら含むハードウェア描画アクセラレータ専用のコマンド シーケンスによって制御が含まれます。

このセクションには、Windows の印刷アーキテクチャについて説明する、次のトピックが含まれています。

[XPSDrv プリンター ドライバー](xpsdrv-printer-drivers.md)

[GDI プリンター ドライバー](gdi-printer-drivers.md)

[印刷チケットと印刷機能のテクノロジ](print-ticket-and-print-capabilities-technologies.md)

[64 ビット プリンター ドライバーの作成](writing-64-bit-printer-drivers.md)

 

 




