---
title: Windows XP でのデータ転送のキャンセル
description: Windows XP でのデータ転送のキャンセル
ms.assetid: 971979a5-950b-49d4-9adb-cd4589a00426
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414fbae7011ee7d291a184d582c0793816c61a48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840877"
---
# <a name="cancellation-of-data-transfers-in-windows-xp"></a>Windows XP でのデータ転送のキャンセル


Microsoft Windows XP および Windows Me では、WIA アプリケーションでデータ転送をキャンセルするには、次の2つの方法がありました。

-   転送コールバックルーチン**IWiaDataCallback:: BandedDataCallback**から S\_FALSE を返します。

-   **Iwiaitemextras:: CancelPendingIO**を呼び出します。 この方法はお勧めしません。インボックスドライバーやサンプルでは使用されません。

また、アプリケーションが転送を取り消したことを WIA ドライバーに通知するには、次の2つの方法がありました。

-   [**IWiaMiniDrvCallBack:: MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)に呼び出された場合は、S\_FALSE を受け取ります。

-   WIA\_イベントを使用して[**IWiaMiniDrv::D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)の呼び出しを受信し、\_IO イベント\_キャンセルします。

Windows XP の実装に関する問題の1つは、2つの通知方法の間に接続がないことです。つまり、ユーザーが**Iwiaitemextras:: CancelPendingIO**を呼び出しても、ドライバーが**IWiaMiniDrv::d rvnotifypnpevent**を使用したデータ転送の非同期キャンセルをサポートしていない場合、アプリケーションは S\_FALSE**を返す必要もあります。IWiaMiniDrvCallBack:: MiniDrvCallback**<em>。</em>

**IWiaDataCallback**および**Iwiaitemextras**インターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。

 

 




