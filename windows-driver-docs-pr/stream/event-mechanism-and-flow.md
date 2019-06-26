---
title: イベント メカニズムとフロー
description: イベント メカニズムとフロー
ms.assetid: 13a6c6fb-3615-44ef-bf01-5003520b3e26
keywords:
- イベントの操作フロー WDK ビデオのキャプチャ
- スキャンの WDK ビデオ キャプチャを終了しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70ecc41adbc8e9b58d2494221089fa2a00ffab08
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384107"
---
# <a name="event-mechanism-and-flow"></a>イベント メカニズムとフロー


**このセクションでは、Microsoft Windows Vista 以降のオペレーティング システムにのみ適用されます。**

ときに、スキャン操作が完了したら、ドライバーに通知イベントを使用してアプリケーションを処理、 **EventData**のメンバー、 [ **KSEVENT\_チューナー\_開始\_スキャン\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)構造体を指定します。 ただし、スキャン操作のドライバーの実際のロックの状態を確認する[ **KSPROPERTY\_チューナー\_スキャン\_状態**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)プロパティを呼び出す必要があります。

カーネル ストリーミング イベント、すべての要求など、アプリケーションで取り消すことができます、 [ **KSEVENT\_チューナー\_開始\_スキャン**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)イベント要求、イベントが完了する前にします。 アプリケーションに現在のスキャン操作、チューナーのフィルターのキャンセルが必要な場合 (*KsTvTune.ax*) 設定、 **StartFrequency**と**EndFrequency**メンバーKSEVENT の\_チューナー\_開始\_スキャン\_ドライバーの KSEVENT への呼び出しで 0 に S\_チューナー\_開始\_スキャンします。 ドライバーは、全体のクリーンアップを実行します。 ただし、ため*KsTvTune.ax*全体のスキャンの別の操作を要求する可能性がドライバーは、全体のクリーンアップを実行しない可能性があります。 スキャン操作をキャンセルする呼び出しは、同期操作です。

アプリケーションが要求すると、スキャンの終了*KsTvTune.ax* KSEVENT を呼び出す\_チューナー\_開始\_によるスキャン**StartFrequency**と**EndFrequency**イベントの登録を解除する 0 に設定します。 ドライバーは、そのワーカー スレッドとその他の内部データ構造の全体のクリーンアップを実行する必要があります。

 

 




