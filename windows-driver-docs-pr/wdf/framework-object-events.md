---
title: フレームワーク オブジェクトのイベント
description: フレームワーク オブジェクトのイベント
ms.assetid: 1bccdd47-8ad6-4607-947f-18c5d2e03038
keywords:
- フレームワークオブジェクト WDK KMDF、イベント
- イベント WDK KMDF
- イベント WDK KMDF、フレームワークオブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d350d7572d7153399b3c4b2911c4ce7f9d545936
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843117"
---
# <a name="framework-object-events"></a>フレームワーク オブジェクトのイベント





一部のフレームワークオブジェクトでは、イベントを生成できます。 フレームワークベースのドライバーは、オブジェクトのイベントのすべて、一部、または一切の通知を受信するように登録できます。 イベントに登録するために、ドライバーはイベントコールバック関数を提供します。 フレームワークは、イベントが発生したときにコールバック関数を呼び出します。

たとえば、ドライバーは、i/o キューに対して[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバック関数を登録できます。 フレームワークは、i/o キューから i/o 要求を削除してドライバーに配信する準備が整うたびに、このコールバック関数を呼び出します。

 

 





