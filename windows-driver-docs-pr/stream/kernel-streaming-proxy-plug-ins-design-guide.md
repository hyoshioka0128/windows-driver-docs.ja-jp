---
title: カーネル ストリーミング プロキシ プラグイン設計ガイド
description: カーネル ストリーミング プロキシ プラグイン設計ガイド
ms.assetid: 9a2b83ab-f54c-421b-bc9b-7dad63cd8cb5
keywords:
- カーネル ストリーミング プロキシ WDK AVStream、プラグイン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48f6ef7ea9e17ef2fd6462597454e5c97336552f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360646"
---
# <a name="kernel-streaming-proxy-plug-ins-design-guide"></a>カーネル ストリーミング プロキシ プラグイン設計ガイド


(KS) プロキシのカーネル ストリーミング モジュール (*Ksproxy.ax*) は、カーネル モードとユーザー モード アプリケーションでオブジェクトを KS 間の通信を仲介する DirectShow フィルター。 ユーザー モード コンポーネントは、KS プロキシを使用して、ミニドライバーに基づいているとの通信に*Ks.sys*します。

具体的には、アプリケーションを制御し、KS ミニドライバーを実装する KS オブジェクトから情報を取得、KS プロキシ モジュールを使用できます。 たとえば、KS フィルター、KS ピン、および KS クロック KS オブジェクトが含めます。

拡張できます KS プロキシ プラグインを記述することでプロパティの値にアクセスするメソッドを提供する COM インターフェイスであります。 プラグイン モデルの利点は、KS pin と KS を直接操作よりもさらになじみのあるメカニズムをアプリケーションの作成者がプロパティ セットをフィルター処理を提供します。

次のセクションでは、KS ベース ミニドライバー KS プロキシと通信するために使用するプロパティ ページまたはプラグイン インターフェイス ハンドラーを記述する方法の概要を説明を提供します。

プラグインのインターフェイスは、プログラムによる制御を取得し、アプリケーション内からプロパティ値の設定を提供します。 また、目標は、ユーザー インターフェイスからプロパティを操作するユーザーを有効にするのには、プロパティ ページを行う方。 両方のメカニズムでは、レジストリを更新することが必要です。

[KS プロキシ プラグインを登録します。](registering-ks-proxy-plug-ins.md)

[プラグインのハンドラーをインターフェイスします。](interface-handler-plug-in.md)

[プラグインのプロパティ ページ](property-page-plug-in.md)

KS プロキシ COM インターフェイス、エクスポートされたヘルパー関数、およびアプリケーションとプラグインで使用される構造に関する詳細については、次を参照してください。[カーネル ストリーミング プロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)します。

 

 




