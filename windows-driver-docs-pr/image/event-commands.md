---
title: イベント コマンド
description: イベント コマンド
ms.assetid: e2b9f985-be57-49a9-b546-5cc74b0b061b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5236cebc751b1351d91e235df20941c6fbfec8fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370042"
---
# <a name="event-commands"></a>イベント コマンド


## <span id="ddk_event_commands_si"></span><span id="DDK_EVENT_COMMANDS_SI"></span>


このセクションのコマンドでは、デバイスのイベントのサポート、microdriver によって使用されます。

<span id="CMD_GET_INTERRUPT_EVENT"></span><span id="cmd_get_interrupt_event"></span>CMD\_取得\_INTERRUPT\_イベント  
デバイスからの割り込みを使用するボタンのイベントの状態を監視する個別のスレッドで、WIA フラット ベッド ドライバーによって呼び出されます (つまり、割り込みパイプ経由でイベントを報告する USB デバイスの場合)。 このコマンドは、実装する必要はありません、デバイスは、ポーリングのみをサポートする場合と E\_NOTIMPL が返される必要があります。

2 つのイベント ハンドルは、microdriver に渡されます。 **LVal**のメンバー、 [ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val) microdriver を使用して通知する必要がありますイベント ハンドルを保持する構造体、 **SetEvent**関数ボタン イベントが発生します。 **処理**VAL 構造体のメンバーは、ドライバーがアンロードされるときに、WIA ベッド ドライバーによって通知されるイベント ハンドルまたはシャット ダウンを保持します。

**PGuid**プッシュされたボタンの GUID を指す VAL 構造体のメンバーを設定する必要があります。 ボタンが押されたない場合に GUID に設定する必要があります\_NULL。

<span id="CMD_STI_GETSTATUS"></span><span id="cmd_sti_getstatus"></span>CMD\_STI\_GETSTATUS  
デバイスのオンライン状態を取得し、デバイスがプッシュ ボタン、ボタンの状態を取得するがかどうかに、WIA ベッド ドライバーによって呼び出されます。

設定、 **lVal**の渡されたメンバー [ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)場合は、デバイスが機能しているオンラインの場合、適切に構造体 1 をします。 場合**lVal**設定されている任意の値 1 以外に、デバイスと見なされ、オフライン、コントロール パネルの デバイスのテストは失敗します。

デバイスがデバイスからの割り込みを使用してボタンをサポートし、ボタンが押された場合、 **pGuid**渡された VAL 構造体のメンバーは、ボタンのイベントの GUID に設定する必要があります。 ポイントのないボタンが押された場合、 **pGuid** GUID 値に\_NULL。 これは、保留中のイベントがないことを通知します。

このコマンドは、デバイスのサポートは、イベントをポーリングまたはデバイスをオンライン状態を表示したい場合に必要です。

 

 





