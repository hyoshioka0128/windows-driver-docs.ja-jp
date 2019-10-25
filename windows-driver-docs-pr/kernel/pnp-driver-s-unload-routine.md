---
title: PnP ドライバーのアンロード ルーチン
description: PnP ドライバーのアンロード ルーチン
ms.assetid: 71b30a84-d3c7-4674-94a6-b99f83567183
keywords:
- アンロードルーチン WDK カーネル、PnP ドライバー
- PnP Unload ルーチンの WDK カーネル
- プラグアンドプレイアンロードルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf0c226fdd2d78a10d9c4bb4bdcd68d58d71ffd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827698"
---
# <a name="pnp-drivers-unload-routine"></a>PnP ドライバーのアンロード ルーチン





PnP ドライバーには、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンによって作成されたドライバー固有のリソース (メモリ、スレッド、イベントなど) を削除する[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンが必要です。 ドライバー固有のリソースを削除する必要がない場合は、ドライバーに*アンロード*ルーチンが含まれている必要がありますが、単にを返すことができます。

ドライバーの*アンロード*ルーチンは、すべてのドライバーのデバイスが削除された後でいつでも呼び出すことができます。 PnP マネージャーは、IRQL = パッシブ\_レベルで、システムスレッドのコンテキストでドライバーの*アンロード*ルーチンを呼び出します。

Pnp ドライバーは、PnP デバイス削除 Irp に応答して、デバイス固有のリソースとデバイスオブジェクトを解放します。 PnP マネージャーは、列挙された各 PnP デバイスに代わってこれらの Irp を送信します。また、ドライバーが[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)を使用して報告する、ルートで列挙されたレガシデバイスも送信します。

そのため、通常、PnP ドライバーの*アンロード*ルーチンは単純であり、多くの場合**return**ステートメントのみで構成されます。 ただし、ドライバーによってドライバー全体のリソースが**Driverentry**ルーチンに割り当てられている場合は、そのリソースを*アンロード*する前に、そのリソースの割り当てを解除する必要があります。 通常、PnP ドライバーのアンロードプロセスは同期操作です。

I/o マネージャーは、ドライバーオブジェクトと、 [**Ioallocatedriverobjectextension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)を使用してドライバーが割り当てたドライバーオブジェクト拡張機能を解放します。

 

 




