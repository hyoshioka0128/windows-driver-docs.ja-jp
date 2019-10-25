---
title: イベントの処理
description: イベントの処理
ms.assetid: 2cd7ccf3-12f5-4ad0-a7c9-a0f437b72445
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、イベント
- streaming ミニドライバー WDK Windows 2000 カーネル、イベント
- ミニドライバー WDK Windows 2000 カーネルストリーミング、イベント
- イベント WDK streaming ミニドライバー
- イベントセット WDK streaming ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91151bbacd9f268cd878d12f277bfd487903c47f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843355"
---
# <a name="handling-events"></a>イベントの処理





ミニドライバーはイベントセットをサポートする場合があります。 デバイス全体と個々のストリームの両方で、イベントを有効または無効にする要求を受け取ることができます。 クラスドライバーは、イベントの有効化と無効化の要求を処理します。 各有効なイベントをキューに置いて、ストリームごとに個別のキューを使用し、デバイスをキューに分割します。 イベントが無効になっている場合は、クラスドライバーによってキューから削除されます。 クラスドライバーは、ミニドライバーが独自の同期を行うかどうかにかかわらず、有効になっている各イベントをキューに記録します。

ミニドライバーは、 [**HW\_ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)構造の**deviceイベント配列**メンバーでサポートされるイベントセットを提供します。 各ストリームは、そのストリームの[**HW\_ストリームの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)構造の**streamイベント配列**でサポートされるイベントセットを提供します。

ミニドライバーは、 [**KSEVENT\_set**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_set)データ構造体を介して処理するイベントセットを定義します。これは、イベントセット内の各イベントに対して1つずつ、 [**KSEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_item)構造の配列を指します。

ミニドライバーは、イベント要求を受け取ることができる場合に、デバイス自体のコールバックと共に、イベント要求を受け取ることができるストリームごとに[*Strminievent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_event_routine)コールバックルーチンを提供します。 *Strminievent*ルーチンが成功以外の状態コードを返す場合、クラスドライバーはイベントをキューに置いていません。

クライアントがイベントを有効にすると、 [**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)構造体が渡されます。この構造体は、イベントが発生した後に通知する方法を記述し、必要に応じてイベント固有のパラメーターを指定します。 クラスドライバーは、要求を受信すると、 [**KSEVENT\_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksevent_entry)構造体を構築して、イベントのトリガー方法を記述します。 各イベントの KSEVENT\_エントリ構造をキューに登録します。 ミニドライバーは、 [**StreamClassGetNextEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetnextevent)ルーチンを使用して、イベントキューを調べることができます。

イベントが実際に発生すると、ミニドライバーは[**StreamClassDeviceNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdevicenotification)または[**Streamclassstreamnotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)を呼び出すことによって、クラスドライバーを通知します。 ミニドライバーは、いくつかの異なる方法でイベントを通知できます。特定のイベントが発生したことを通知したり、特定の種類のすべてのイベントが発生したことを通知したりすることができます。 詳細については、「 **StreamClassDeviceNotification** 」または「 **Streamclassstreamnotification** 」を参照してください。

クラスドライバーは、 [**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)構造体を解析して[**KSEVENT\_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksevent_entry)構造体を作成できますが、元の要求の後に続くイベント固有のパラメーターに対して同じ操作を行うことはできません。 ミニドライバーは、イベントの宣言に使用された KSEVENT\_項目の**ExtraEntryData**メンバーに0以外の値を指定することによって、特定の種類のイベントの KSEVENT\_エントリ構造の後に追加の領域を割り当てることができます。 この種類のイベントに対して*Strminievent*が呼び出されると、KSEVENTDATA からのイベント固有のパラメーターをこのメモリに格納する必要があります。

 

 




