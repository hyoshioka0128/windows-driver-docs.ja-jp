---
title: イベントコマンド
description: イベントコマンド
ms.assetid: e2b9f985-be57-49a9-b546-5cc74b0b061b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fe14e4edb32a705cc56e882cd1499345df5728c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840842"
---
# <a name="event-commands"></a>イベントコマンド


## <span id="ddk_event_commands_si"></span><span id="DDK_EVENT_COMMANDS_SI"></span>


このセクションのコマンドは、デバイスイベントをサポートするためにマイクロドライバーによって使用されます。

<span id="CMD_GET_INTERRUPT_EVENT"></span><span id="cmd_get_interrupt_event"></span>CMD\_\_割り込み\_イベントの取得  
デバイスからの割り込みを使用するボタンイベント (つまり、割り込みパイプを介してイベントを報告する USB デバイス) の状態を監視するために、別のスレッドで WIA フラットドライブによって呼び出されます。 デバイスでポーリングしかサポートされていない場合は、このコマンドを実装する必要はなく、E\_NOTIMPL を返す必要があります。

マイクロドライバーには、2つのイベントハンドルが渡されます。 [**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーは、ボタンイベントが発生したときに、 **SetEvent**関数を使用してマイクロドライバーによって通知されるイベントハンドルを保持します。 VAL 構造体の**handle**メンバーは、ドライバーがアンロードまたはシャットダウンされるときに、WIA フラット化ドライバーによって通知されるイベントハンドルを保持します。

VAL 構造体の**Pguid**メンバーは、プッシュされたボタンの GUID を指すように設定する必要があります。 押されたボタンがない場合は、GUID\_NULL に設定する必要があります。

<span id="CMD_STI_GETSTATUS"></span><span id="cmd_sti_getstatus"></span>CMD\_STI\_GETSTATUS  
WIA フラット化ドライバーによって呼び出され、デバイスのオンライン状態を取得します。デバイスにプッシュボタンがある場合は、ボタンの状態を取得します。

デバイスがオンラインで、正常に機能している場合は、渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーを1に設定します。 **LVal**が1以外の値に設定されている場合、デバイスはオフラインと見なされ、コントロールパネルのデバイステストに失敗します。

デバイスの割り込みを使用しないボタンがデバイスでサポートされていて、ボタンが押されている場合は、渡された VAL 構造体の**Pguid**メンバーをボタンイベントの guid に設定する必要があります。 ボタンが押されていない場合は、 **Pguid**を値 GUID\_NULL にします。 これにより、保留中のイベントがないことが通知されます。

デバイスでポーリングイベントがサポートされている場合、またはデバイスで状態を表示する場合は、このコマンドが必要です。

 

 





