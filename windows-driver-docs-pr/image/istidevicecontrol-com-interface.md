---
title: IStiDeviceControl COM インターフェイス
description: IStiDeviceControl COM インターフェイス
ms.assetid: 6d98f5d7-c471-4abb-8e69-dbac3d336c2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db78f1489815a71dbe223fc2ec4922416178e88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378932"
---
# <a name="istidevicecontrol-com-interface"></a>IStiDeviceControl COM インターフェイス





**IStiDeviceControl** COM インターフェイスを提供します[ユーザー モードのままイメージ ミニドライバー](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)内に格納された情報にアクセスして、[イメージ イベント モニターではまだ](overview-of-sti-components.md#ddk-still-image-event-monitor-si)します。 また、ミニドライバーは、静止画像エラー ログに情報を書き込むこともできます。

によって定義されたメソッド、 **IStiDeviceControl**インターフェイスには、次が含まれます。

<a href="" id="istidevicecontrol--addref"></a>[**IStiDeviceControl::AddRef**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-addref)  
インクリメント、 **IStiDeviceControl**インターフェイスの参照カウントします。

<a href="" id="istidevicecontrol--getmydeviceopenmode"></a>[**IStiDeviceControl::GetMyDeviceOpenMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceopenmode)  
静止画像デバイスのインスタンスが作成されたときに、アプリケーションが指定されている転送モードを取得する静止画像ミニドライバーを使用できます。

<a href="" id="istidevicecontrol--getmydeviceportname"></a>[**IStiDeviceControl::GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)  
デバイスのポートの名前を取得する静止画像ミニドライバーを使用できます。

<a href="" id="istidevicecontrol--release"></a>[**IStiDeviceControl::Release**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-release)  
定義するインスタンスの COM オブジェクトを閉じ、 **IStiDeviceControl**インターフェイス、およびインターフェイスへのアクセスを削除します。

<a href="" id="istidevicecontrol--writetoerrorlog"></a>[**IStiDeviceControl::WriteToErrorLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-writetoerrorlog)  
イメージは引き続き、エラー ログにメッセージを書き込む静止画像ミニドライバーを使用できます。

 

 




