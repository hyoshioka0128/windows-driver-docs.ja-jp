---
title: フレームワーク オブジェクトのイベント
description: フレームワーク オブジェクトのイベント
ms.assetid: 1bccdd47-8ad6-4607-947f-18c5d2e03038
keywords:
- framework オブジェクト WDK KMDF、イベント
- WDK KMDF イベント
- WDK KMDF、framework のオブジェクトのイベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f41801439af005811faad1a10ec1c231e7e9e7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384457"
---
# <a name="framework-object-events"></a>フレームワーク オブジェクトのイベント





一部のフレームワーク オブジェクトには、イベントを生成できます。 フレームワーク ベースのドライバーは、すべての通知を受信登録できます some、またはオブジェクトのイベントのいずれもします。 イベントを登録するには、ドライバーは、イベントのコールバック関数を提供します。 フレームワークは、イベントの発生時に、コールバック関数を呼び出します。

たとえば、ドライバーが登録できる、 [ *EvtIoDefault* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default) I/O キューのコールバック関数。 フレームワークによりはこのコールバック関数は、framework が I/O キューから、I/O 要求を削除し、ドライバーに配信するたびに呼び出します。

 

 





