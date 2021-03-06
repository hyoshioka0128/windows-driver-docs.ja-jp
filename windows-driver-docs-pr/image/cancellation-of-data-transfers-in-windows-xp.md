---
title: Windows XP でのデータ転送のキャンセル
description: Windows XP でのデータ転送のキャンセル
ms.assetid: 971979a5-950b-49d4-9adb-cd4589a00426
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d19f8bd536be05a1494833545799614c9528ae1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355513"
---
# <a name="cancellation-of-data-transfers-in-windows-xp"></a>Windows XP でのデータ転送のキャンセル


Microsoft Windows XP と Windows Me、WIA アプリケーション データの転送をキャンセルする 2 つの方法がありました。

-   戻り値の S\_転送コールバック ルーチンから FALSE **IWiaDataCallback::BandedDataCallback**します。

-   呼び出す**IWiaItemExtras::CancelPendingIO**します。 このメソッドはお勧めしませんし、インボックス ドライバーやサンプルでは使用されません。

また、WIA ドライバー、アプリケーションが、転送をキャンセルした通知を受け取る方法は 2 つが発生しました。

-   受信 S\_に呼び出されると FALSE [ **IWiaMiniDrvCallBack::MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)します。

-   呼び出しを受け取るその[ **IWiaMiniDrv::drvNotifyPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent) WIA を\_イベント\_キャンセル\_IO イベント。

Windows XP 導入の問題の 1 つは、2 つの通知方法; の間の接続がないです。つまり、ユーザーが呼び出す場合**IWiaItemExtras::CancelPendingIO** 、ドライバーは経由のデータ転送の非同期のキャンセルをサポートしていませんが、 **IWiaMiniDrv::drvNotifyPnPEvent**アプリケーションは返す必要も S\_から FALSE **IWiaMiniDrvCallBack::MiniDrvCallback**<em>します。</em>

**IWiaDataCallback**と**IWiaItemExtras**インターフェイスが、Microsoft Windows SDK ドキュメントに記載されています。

 

 




