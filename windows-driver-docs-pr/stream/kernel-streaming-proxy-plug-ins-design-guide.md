---
title: カーネル ストリーミング プロキシ プラグイン設計ガイド
description: カーネル ストリーミング プロキシ プラグイン設計ガイド
ms.assetid: 9a2b83ab-f54c-421b-bc9b-7dad63cd8cb5
keywords:
- カーネルストリーミングプロキシ WDK AVStream、プラグイン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec4a8b8641b6b7df567babb0f6f9f85c7f7657e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845561"
---
# <a name="kernel-streaming-proxy-plug-ins-design-guide"></a>カーネル ストリーミング プロキシ プラグイン設計ガイド


カーネルストリーミング (KS) プロキシモジュール (*Ksproxy.ax*) は、カーネルモードとユーザーモードのアプリケーションで ks オブジェクト間の通信を仲介する DirectShow フィルターです。 ユーザーモードコンポーネントでは、ks プロキシを使用して、ミニドライバーに基づくすべてのと通信*できます。*

具体的には、アプリケーションは ks プロキシモジュールを使用して、ks ミニドライバーが実装する KS オブジェクトの情報を制御および取得できます。 KS オブジェクトには、たとえば KS フィルター、KS ピン、KS クロックなどがあります。

KS プロキシは、プロパティ値にアクセスするメソッドを提供する COM インターフェイスであるプラグインを記述することによって拡張できます。 プラグインモデルの利点は、KS ピンおよび KS フィルターのプロパティセットを直接操作するよりも使い慣れたメカニズムをアプリケーションライターに提供できることです。

次のセクションでは、ks プロキシを使用して KS ベースのミニドライバーと通信するインターフェイスハンドラープラグインまたはプロパティページを記述する方法について、概要を説明します。

インターフェイスプラグインは、アプリケーション内からプロパティ値を取得および設定するためのプログラムによる制御を提供します。 または、ユーザーがユーザーインターフェイスを使用してプロパティを操作できるようにすることが目的の場合は、プロパティページの方がわかりやすくなります。 どちらのメカニズムでも、レジストリを更新する必要があります。

[KS プロキシプラグインを登録しています](registering-ks-proxy-plug-ins.md)

[インターフェイスハンドラープラグイン](interface-handler-plug-in.md)

[プロパティページプラグイン](property-page-plug-in.md)

アプリケーションとプラグインで使用される KS プロキシ COM インターフェイス、エクスポートされたヘルパー関数、および構造体の詳細については、「[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。

 

 




