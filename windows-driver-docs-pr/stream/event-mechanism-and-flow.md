---
title: イベント メカニズムとフロー
description: イベント メカニズムとフロー
ms.assetid: 13a6c6fb-3615-44ef-bf01-5003520b3e26
keywords:
- イベント操作フロー WDK ビデオキャプチャ
- WDK ビデオキャプチャのスキャンを終了しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76fb8256d748ae13a389e8256916229d68c10441
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834421"
---
# <a name="event-mechanism-and-flow"></a>イベント メカニズムとフロー


**このセクションは、Microsoft Windows Vista 以降のオペレーティングシステムにのみ適用されます。**

スキャン操作が完了すると、ドライバーはイベントハンドルを介してアプリケーションに通知します。これは、KSEVENT\_チューナーの**EventData**メンバーが[ **\_スキャン\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)が指定した\_開始することを示します。 ただし、スキャン操作の実際のロック状態を確認するには、ドライバーの[**Ksk プロパティ\_チューナー\_scan\_status**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)プロパティを呼び出す必要があります。

すべてのカーネルストリーミングイベント要求と同様に、アプリケーションは KSEVENT\_チューナーをキャンセルして、イベントが完了する前にイベント要求の[ **\_スキャンを開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)ことができます。 アプリケーションで現在のスキャン操作をキャンセルする必要がある場合、チューナーフィルター (*KsTvTune.ax*) は KSEVENT\_チューナーの**Startfrequency**および**endfrequency**メンバーを設定し\_\_スキャン\_S をゼロに設定し、ドライバーの KSEVENT\_チューナーを呼び出して\_スキャンを開始します。\_ ドライバーはクリーンアップ全体を実行する可能性があります。 ただし、 *KsTvTune.ax*はスキャン操作全体を要求する場合があるので、ドライバーはクリーンアップ全体を実行しない可能性があります。 スキャン操作をキャンセルする呼び出しは同期操作です。

アプリケーションがスキャンを終了する必要がある場合、 *KsTvTune.ax*は KSEVENT\_チューナー\_呼び出します。 **Startfrequency**と**endfrequency**を0に設定して、イベントの登録を解除し\_スキャンを開始します。 次に、ドライバーは、ワーカースレッドとその他の内部データ構造のクリーンアップ全体を実行する必要があります。

 

 




