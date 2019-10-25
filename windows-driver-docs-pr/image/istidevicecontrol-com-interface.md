---
title: IStiDeviceControl COM インターフェイス
description: IStiDeviceControl COM インターフェイス
ms.assetid: 6d98f5d7-c471-4abb-8e69-dbac3d336c2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 623cef89bce3c950bdbae3fd1cdd2f5379eaebb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840808"
---
# <a name="istidevicecontrol-com-interface"></a>IStiDeviceControl COM インターフェイス





**Iミニドライバー Devicecontrol** COM インターフェイスは、[静止イメージイベントモニター](overview-of-sti-components.md#ddk-still-image-event-monitor-si)内に格納されている情報にアクセスできる、[ユーザーモードの静止画像](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)を提供します。 また、ミニドライバーが静止イメージのエラーログに情報を書き込むこともできます。

**Iの Devicecontrol**インターフェイスによって定義されるメソッドには、次のものがあります。

<a href="" id="istidevicecontrol--addref"></a>[**I-Devicecontrol:: AddRef**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-addref)  
**Iの Devicecontrol**インターフェイスの参照カウントをインクリメントします。

<a href="" id="istidevicecontrol--getmydeviceopenmode"></a>[**I、Devicecontrol:: GetMyDeviceOpenMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceopenmode)  
静止イメージデバイスのインスタンスを作成したときに、アプリケーションが指定した転送モードをミニドライバーに取得できるようにします。

<a href="" id="istidevicecontrol--getmydeviceportname"></a>[**I、Devicecontrol:: GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)  
静止イメージミニドライバーがデバイスのポート名を取得できるようにします。

<a href="" id="istidevicecontrol--release"></a>[**Iの Devicecontrol:: Release**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-release)  
**Iの Devicecontrol**インターフェイスを定義するインスタンス COM オブジェクトを閉じ、インターフェイスへのアクセスを削除します。

<a href="" id="istidevicecontrol--writetoerrorlog"></a>[**IStiDeviceControl:: WriteToErrorLog ログ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-writetoerrorlog)  
静止画像ミニドライバーが静止画像エラーログにメッセージを書き込むことを許可します。

 

 




