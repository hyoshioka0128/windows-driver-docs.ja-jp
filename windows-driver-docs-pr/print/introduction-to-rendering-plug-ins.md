---
title: レンダリング プラグインの概要
description: レンダリング プラグインの概要
ms.assetid: 7e6756ca-822a-4386-bcbd-363a10b1b2a3
keywords:
- プラグインを WDK の印刷、レンダリング プラグインに関するレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de9f3f3b8a1eaada94961329a2b9010eed22c646
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385397"
---
# <a name="introduction-to-rendering-plug-ins"></a>レンダリング プラグインの概要





いずれかに新しいプリンター デバイスのサポートを追加すると、 [Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md) (Unidrv) または[Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md) (Pscript) COM インターフェイスのメソッドを実装することができます印刷スプーラにドライバーを送信するデータを変更します。

ユーザー モード DLL を提供することで、このカスタマイズを実現します。 この DLL と呼ばれます、*プラグインでレンダリング*します。

次の 2 つの種類のカスタマイズをサポートします。

-   一部のグラフィックスのカスタマイズされたバージョン DDI レンダリング関数を提供します。

-   表示されるイメージやスキャン ライン データ ストリームを変更またはデータ ストリームは、スプーラーに送信する前に、Postscript コードを特定の挿入ポイントに挿入する Unidrv 固有または Pscript に固有の COM インターフェイス メソッドを実装します。

**注**  プラグインを表示する必要がありますしない生成ウィンドウを直接します。 Windows Vista 以降、非同期のユーザー通知の XML スキーマを使用してクライアント コンピューターに非同期のイベント通知メッセージを行うことができます asyncui.xsd します。 詳細については、次を参照してください[非同期のユーザー通知スキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/asynchronous-user-notification-schema)。

 

 

 




