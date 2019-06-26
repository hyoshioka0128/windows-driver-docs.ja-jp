---
title: イベントの処理
description: イベントの処理
ms.assetid: 2cd7ccf3-12f5-4ad0-a7c9-a0f437b72445
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネル、イベント
- ミニドライバー WDK Windows 2000 のカーネル、イベントのストリーミング
- WDK Windows 2000 のカーネル イベントのストリーミング、ミニドライバー
- WDK ストリーミング ミニドライバーのイベント
- イベントは、WDK のミニドライバーのストリーミングを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 406a314e355560c2e3f80d1d235626e3f074133c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384024"
---
# <a name="handling-events"></a>イベントの処理





ミニドライバーは、イベントのセットをサポート可能性があります。 両方の整数部と個々 のストリームとして、デバイスが有効にまたはイベントを無効にする要求を受信できます。 ドライバーの処理イベントのクラスが有効にし、要求を無効にします。 別のキューを使用している、各ストリームと、デバイスで、有効になっている各イベントをキューします。 イベントを無効にすると、クラス ドライバーにより、キューから削除します。 ミニドライバーは、独自の同期かどうかは、クラス ドライバーが、有効になっている各イベントをキューに注意してください。

ミニドライバーは、イベントのセットでサポートを提供、 **DeviceEventsArray**のメンバー、 [ **HW\_ストリーム\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_header)構造体。 各ストリームでは、イベントのセットを提供する、 **StreamEventsArray**の[ **HW\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_information)を構造体ストリーム。

ミニドライバーは、イベントのセットを介して処理を定義、 [ **KSEVENT\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_set)データ構造体の配列を指す順番[ **KSEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_item)構造体、イベントごとに 1 つのイベント セットにします。

ミニドライバーは、 [ *StrMiniEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_event_routine)各ストリーム イベントの要求を受信できる場合、デバイス自体のコールバックとイベントの要求を受け取ることができるコールバック ルーチン。 場合、 *StrMiniEvent*ルーチンには、成功以外のステータス コードが返されます、クラス ドライバーをイベント キューに登録されます。

イベントの有効化要求は、クライアントの際に渡して、 [ **KSEVENTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)構造体は、これが発生した場合のイベントの通知方法を説明するには、必要に応じて後にイベント固有のパラメーター。 ビルド クラス ドライバーは、要求を受け取る、 [ **KSEVENT\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksevent_entry)構造体をイベントをトリガーする方法について説明します。 キュー、KSEVENT\_イベントごとにエントリの構造体。 使用できるようにミニドライバー、 [ **StreamClassGetNextEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassgetnextevent)ルーチンをイベント キューを確認します。

実際には、イベントの発生時に、ミニドライバーがいずれかを呼び出してクラス ドライバーを通知[ **StreamClassDeviceNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassdevicenotification)または[ **StreamClassStreamNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification). ミニドライバーは、いくつかの方法でイベントを通知できます。 そのこと、特定のイベントが発生しました、または、特定の種類のすべてのイベントが発生したことを知らせることを通知できます。 参照してください**StreamClassDeviceNotification**または**StreamClassStreamNotification**詳細についてはします。

クラスのドライバーを解析できます、 [ **KSEVENTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)構造を作成するその[ **KSEVENT\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksevent_entry)構造が、以下のことはできません元の要求内のイベントに固有のパラメーターの同じ操作を行います。 KSEVENT 後に追加の領域を割り当てることができます、ミニドライバー\_以外の値を提供することで、イベントの特定の種類のエントリの構造、 **ExtraEntryData** 、KSEVENT のメンバー\_項目するために使用イベントを宣言します。 ときに*StrMiniEvent*と呼ばれる、イベントの種類、このメモリに KSEVENTDATA からのイベントに固有のパラメーターが格納される必要があります。

 

 




