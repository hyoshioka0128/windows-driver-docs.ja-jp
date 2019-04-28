---
title: デバイス メタデータの読み取り
description: デバイス メタデータの読み取り
ms.assetid: 402de9de-8bfe-4cc2-9b8e-06e0ad925eb1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b6a3e9a710c66073199cbd743df7325ccac19d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379615"
---
# <a name="reading-device-metadata"></a>デバイス メタデータの読み取り


Web サービス スキャナーの WIA ミニドライバーは、実行時に、次のデバイス メタデータのプロパティを読み取る必要があります。

<a href="" id="pkey-pnpx-serviceid"></a>**鍵\_PNPX\_ServiceId**  
このプロパティが初期化に必要な[ **WIA\_DPS\_サービス\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551428) WIA プロパティ。

<a href="" id="pkey-pnpx-globalidentity"></a>**鍵\_PNPX\_GlobalIdentity**  
このプロパティを初期化します、 [ **WIA\_DPS\_GLOBAL\_IDENTITY** ](https://msdn.microsoft.com/library/windows/hardware/ff551395) WIA プロパティ。

<a href="" id="pkey-pnpx-id--directly-or-indirectly-by-using-istidevicecontrol--getmydeviceportname-"></a>**鍵\_PNPX\_ID** (を使用して直接または間接的に[ **IStiDeviceControl::GetMyDevicePortName**](https://msdn.microsoft.com/library/windows/hardware/ff542944))  
このプロパティを初期化します、 [ **WIA\_DPS\_デバイス\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551374)デバイス プロパティ。

ミニドライバーは、次を含むその他のプロパティを読み取るも可能性があります。

<a href="" id="pkey-pnpx-firmware-version"></a>**鍵\_PNPX\_ファームウェア\_バージョン**  
このプロパティを初期化します、 [ **WIA\_DPA\_ファームウェア\_バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff550309) WIA プロパティ。

**注**  を使用して、ミニドライバー *WSDScan.sys*呼び出して PNPX ID 値を取得できますも[ **IStiDeviceControl::GetMyDevicePortName** ](https://msdn.microsoft.com/library/windows/hardware/ff542944);返されるデバイス パスは現在鍵\_PNPX\_id。

 

これらの鍵の説明については\_PNPX\_*Xxx*プロパティを参照してください、 [PNP X 実行者ガイド](https://go.microsoft.com/fwlink/p/?linkid=242570)します。

次のコード例では、ストアからデバイスのプロパティを読み取る方法と、前のセクションで説明されているように取得した現在の関数インスタンス オブジェクトのプロパティ ストアを開く方法を示します。

[プロパティ ストアを開くためのコード例](code-example-for-opening-a-property-store.md)

[デバイスのプロパティを読み取るためのコード例](code-example-for-reading-device-properties.md)

[デバイスのプロパティを初期化するためのコード例](code-example-for-initializing-device-properties.md)

 

 




