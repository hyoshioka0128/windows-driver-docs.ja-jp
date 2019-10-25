---
title: デバイス メタデータの読み取り
description: デバイス メタデータの読み取り
ms.assetid: 402de9de-8bfe-4cc2-9b8e-06e0ad925eb1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca3fe282e179ca0ad3985194adcb1c6b577b651
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840764"
---
# <a name="reading-device-metadata"></a>デバイス メタデータの読み取り


Web サービススキャナーの WIA ミニドライバーは、実行時に次のデバイスメタデータプロパティを読み取る必要があります。

<a href="" id="pkey-pnpx-serviceid"></a>**PKEY\_PNPX\_ServiceId**  
このプロパティは、 [**wia\_DPS\_SERVICE\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-service-id) wia プロパティを初期化するために必要です。

<a href="" id="pkey-pnpx-globalidentity"></a>**PKEY\_PNPX\_GlobalIdentity**  
このプロパティにより、 [**wia\_DPS\_グローバル\_id**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-global-identity)の wia プロパティが初期化されます。

<a href="" id="pkey-pnpx-id--directly-or-indirectly-by-using-istidevicecontrol--getmydeviceportname-"></a>**PKEY\_PNPX\_ID** ( [**iGetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)を使用して直接または間接的に)  
このプロパティは、 [**WIA\_DPS\_device\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-device-id)デバイスプロパティを初期化します。

ミニドライバーは、次のような他のプロパティも読み取ることができます。

<a href="" id="pkey-pnpx-firmware-version"></a>**PKEY\_PNPX\_ファームウェア\_バージョン**  
このプロパティは、 [**wia の\_DPA\_ファームウェア\_VERSION**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-firmware-version) wia プロパティを初期化します。

*WSDScan*を使用するミニドライバーでは、 [**Istidevicecontrol:: GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname); を呼び出して、pnpx ID 値を取得することもできます **。  ** 返されるデバイスパスは、現在の PKEY\_PNPX\_ID です。

 

これらの PKEY\_PNPX\_*Xxx*プロパティの詳細については、「 [pnp-x 実装ガイド](https://go.microsoft.com/fwlink/p/?linkid=242570)」を参照してください。

次のコード例は、前のセクションで説明したように取得された現在の関数インスタンスオブジェクトのプロパティストアを開き、ストアからデバイスプロパティを読み取る方法を示しています。

[プロパティストアを開くためのコード例](code-example-for-opening-a-property-store.md)

[デバイスプロパティを読み取るためのコード例](code-example-for-reading-device-properties.md)

[デバイスプロパティを初期化するためのコード例](code-example-for-initializing-device-properties.md)

 

 




