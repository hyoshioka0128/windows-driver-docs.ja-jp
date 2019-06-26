---
title: デバイス メタデータの読み取り
description: デバイス メタデータの読み取り
ms.assetid: 402de9de-8bfe-4cc2-9b8e-06e0ad925eb1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f159226170ede9a053dde1aa19d7f530fff1123
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374293"
---
# <a name="reading-device-metadata"></a>デバイス メタデータの読み取り


Web サービス スキャナーの WIA ミニドライバーは、実行時に、次のデバイス メタデータのプロパティを読み取る必要があります。

<a href="" id="pkey-pnpx-serviceid"></a>**鍵\_PNPX\_ServiceId**  
このプロパティが初期化に必要な[ **WIA\_DPS\_サービス\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-service-id) WIA プロパティ。

<a href="" id="pkey-pnpx-globalidentity"></a>**鍵\_PNPX\_GlobalIdentity**  
このプロパティを初期化します、 [ **WIA\_DPS\_GLOBAL\_IDENTITY** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-global-identity) WIA プロパティ。

<a href="" id="pkey-pnpx-id--directly-or-indirectly-by-using-istidevicecontrol--getmydeviceportname-"></a>**鍵\_PNPX\_ID** (を使用して直接または間接的に[ **IStiDeviceControl::GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname))  
このプロパティを初期化します、 [ **WIA\_DPS\_デバイス\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-device-id)デバイス プロパティ。

ミニドライバーは、次を含むその他のプロパティを読み取るも可能性があります。

<a href="" id="pkey-pnpx-firmware-version"></a>**鍵\_PNPX\_ファームウェア\_バージョン**  
このプロパティを初期化します、 [ **WIA\_DPA\_ファームウェア\_バージョン**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-firmware-version) WIA プロパティ。

**注**  を使用して、ミニドライバー *WSDScan.sys*呼び出して PNPX ID 値を取得できますも[ **IStiDeviceControl::GetMyDevicePortName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname);返されるデバイス パスは現在鍵\_PNPX\_id。

 

これらの鍵の説明については\_PNPX\_*Xxx*プロパティを参照してください、 [PNP X 実行者ガイド](https://go.microsoft.com/fwlink/p/?linkid=242570)します。

次のコード例では、ストアからデバイスのプロパティを読み取る方法と、前のセクションで説明されているように取得した現在の関数インスタンス オブジェクトのプロパティ ストアを開く方法を示します。

[プロパティ ストアを開くためのコード例](code-example-for-opening-a-property-store.md)

[デバイスのプロパティを読み取るためのコード例](code-example-for-reading-device-properties.md)

[デバイスのプロパティを初期化するためのコード例](code-example-for-initializing-device-properties.md)

 

 




