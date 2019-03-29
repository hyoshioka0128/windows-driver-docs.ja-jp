---
title: Windows XP でのデータ転送のキャンセル
description: Windows XP でのデータ転送のキャンセル
ms.assetid: 971979a5-950b-49d4-9adb-cd4589a00426
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6741c9564485a42ca0753be033d9542422c9b38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570189"
---
# <a name="cancellation-of-data-transfers-in-windows-xp"></a>Windows XP でのデータ転送のキャンセル


Microsoft Windows XP と Windows Me、WIA アプリケーション データの転送をキャンセルする 2 つの方法がありました。

-   戻り値の S\_転送コールバック ルーチンから FALSE **IWiaDataCallback::BandedDataCallback**します。

-   呼び出す**IWiaItemExtras::CancelPendingIO**します。 このメソッドはお勧めしませんし、インボックス ドライバーやサンプルでは使用されません。

また、WIA ドライバー、アプリケーションが、転送をキャンセルした通知を受け取る方法は 2 つが発生しました。

-   受信 S\_に呼び出されると FALSE [ **IWiaMiniDrvCallBack::MiniDrvCallback**](https://msdn.microsoft.com/library/windows/hardware/ff543946)します。

-   呼び出しを受け取るその[ **IWiaMiniDrv::drvNotifyPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998) WIA を\_イベント\_キャンセル\_IO イベント。

Windows XP 導入の問題の 1 つは、2 つの通知方法; の間の接続がないです。つまり、ユーザーが呼び出す場合**IWiaItemExtras::CancelPendingIO** 、ドライバーは経由のデータ転送の非同期のキャンセルをサポートしていませんが、 **IWiaMiniDrv::drvNotifyPnPEvent**アプリケーションは返す必要も S\_から FALSE **IWiaMiniDrvCallBack::MiniDrvCallback**<em>します。</em>

**IWiaDataCallback**と**IWiaItemExtras**インターフェイスが、Microsoft Windows SDK ドキュメントに記載されています。

 

 




