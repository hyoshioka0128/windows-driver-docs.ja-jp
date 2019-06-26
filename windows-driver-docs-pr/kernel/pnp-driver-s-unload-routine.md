---
title: PnP ドライバーのアンロード ルーチン
description: PnP ドライバーのアンロード ルーチン
ms.assetid: 71b30a84-d3c7-4674-94a6-b99f83567183
keywords:
- ルーチンの WDK カーネルをアンロード、PnP ドライバー
- PnP WDK カーネルの日常的なアンロード
- プラグ アンド プレイ アンロード ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcc8430d2035ba3320e72a69a31738e8d8997782
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369727"
---
# <a name="pnp-drivers-unload-routine"></a>PnP ドライバーのアンロード ルーチン





PnP ドライバーが必要、 [*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)など、メモリ、スレッド、およびイベントは、によって作成されるすべてのドライバー固有のリソースを削除するルーチン、 [ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。 ドライバーがありますを削除するドライバー固有のリソースがない場合、*アンロード*ルーチンを返すだけです。

ドライバーの*アンロード*ルーチンは、すべてのドライバーのデバイスが削除された後、いつでも呼び出すことができます。 PnP マネージャーには、ドライバーの*アンロード*IRQL でシステムのスレッドのコンテキストで日常的なパッシブ =\_レベル。

PnP ドライバーでは、デバイスに固有のリソースとデバイスの削除の Irp の PnP への応答内のデバイス オブジェクトを解放します。 PnP マネージャーこれら Irp に代わって送信各が列挙ルート列挙とするレガシ デバイスとドライバーの PnP デバイスのレポートを使用して[ **IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioreportdetecteddevice)します。

その結果、*アンロード*PnP ドライバーのルーチンは、通常は単純で、多くの場合のみで構成される、**返す**ステートメント。 ただし、ドライバーがドライバー全体のリソースを割り当てられている場合、 **DriverEntry**日常的なその必要がありますの割り当てを解除でそれらのリソースの*アンロード*それが既に完了しない限り、日常的な。 一般に、PnP ドライバーをアンロードするプロセスでは、同期操作です。

I/O マネージャーがドライバー オブジェクトとドライバー オブジェクトの拡張機能を使用して、ドライバーの割り当てを解放[ **IoAllocateDriverObjectExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatedriverobjectextension)します。

 

 




