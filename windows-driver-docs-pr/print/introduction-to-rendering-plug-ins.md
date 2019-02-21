---
title: プラグインのレンダリングの概要
description: プラグインのレンダリングの概要
ms.assetid: 7e6756ca-822a-4386-bcbd-363a10b1b2a3
keywords:
- プラグインを WDK の印刷、レンダリング プラグインに関するレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cb9467f0a4797426f8a9707e1737df2775e92e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536047"
---
# <a name="introduction-to-rendering-plug-ins"></a>プラグインのレンダリングの概要





いずれかに新しいプリンター デバイスのサポートを追加すると、 [Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md) (Unidrv) または[Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md) (Pscript) COM インターフェイスのメソッドを実装することができます印刷スプーラにドライバーを送信するデータを変更します。

ユーザー モード DLL を提供することで、このカスタマイズを実現します。 この DLL と呼ばれます、*プラグインでレンダリング*します。

次の 2 つの種類のカスタマイズをサポートします。

-   一部のグラフィックスのカスタマイズされたバージョン DDI レンダリング関数を提供します。

-   表示されるイメージやスキャン ライン データ ストリームを変更またはデータ ストリームは、スプーラーに送信する前に、Postscript コードを特定の挿入ポイントに挿入する Unidrv 固有または Pscript に固有の COM インターフェイス メソッドを実装します。

**注**  プラグインを表示する必要がありますしない生成ウィンドウを直接します。 Windows Vista 以降、非同期のユーザー通知の XML スキーマを使用してクライアント コンピューターに非同期のイベント通知メッセージを行うことができます asyncui.xsd します。 詳細については、次を参照してください[非同期のユーザー通知スキーマ](https://msdn.microsoft.com/library/windows/hardware/ff545066).。

 

 

 




