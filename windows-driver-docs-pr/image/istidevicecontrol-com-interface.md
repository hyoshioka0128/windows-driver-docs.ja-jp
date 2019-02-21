---
title: IStiDeviceControl COM インターフェイス
description: IStiDeviceControl COM インターフェイス
ms.assetid: 6d98f5d7-c471-4abb-8e69-dbac3d336c2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c6daee1b03f6da3082b9959cb95485d0ea21b18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560296"
---
# <a name="istidevicecontrol-com-interface"></a>IStiDeviceControl COM インターフェイス





**IStiDeviceControl** COM インターフェイスを提供します[ユーザー モードのままイメージ ミニドライバー](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)内に格納された情報にアクセスして、[イメージ イベント モニターではまだ](overview-of-sti-components.md#ddk-still-image-event-monitor-si)します。 また、ミニドライバーは、静止画像エラー ログに情報を書き込むこともできます。

によって定義されたメソッド、 **IStiDeviceControl**インターフェイスには、次が含まれます。

<a href="" id="istidevicecontrol--addref"></a>[**IStiDeviceControl::AddRef**](https://msdn.microsoft.com/library/windows/hardware/ff542933)  
インクリメント、 **IStiDeviceControl**インターフェイスの参照カウントします。

<a href="" id="istidevicecontrol--getmydeviceopenmode"></a>[**IStiDeviceControl::GetMyDeviceOpenMode**](https://msdn.microsoft.com/library/windows/hardware/ff542942)  
静止画像デバイスのインスタンスが作成されたときに、アプリケーションが指定されている転送モードを取得する静止画像ミニドライバーを使用できます。

<a href="" id="istidevicecontrol--getmydeviceportname"></a>[**IStiDeviceControl::GetMyDevicePortName**](https://msdn.microsoft.com/library/windows/hardware/ff542944)  
デバイスのポートの名前を取得する静止画像ミニドライバーを使用できます。

<a href="" id="istidevicecontrol--release"></a>[**IStiDeviceControl::Release**](https://msdn.microsoft.com/library/windows/hardware/ff543725)  
定義するインスタンスの COM オブジェクトを閉じ、 **IStiDeviceControl**インターフェイス、およびインターフェイスへのアクセスを削除します。

<a href="" id="istidevicecontrol--writetoerrorlog"></a>[**IStiDeviceControl::WriteToErrorLog**](https://msdn.microsoft.com/library/windows/hardware/ff543727)  
イメージは引き続き、エラー ログにメッセージを書き込む静止画像ミニドライバーを使用できます。

 

 




