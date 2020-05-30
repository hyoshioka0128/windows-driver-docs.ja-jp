---
title: デバイス メタデータの読み取り
description: デバイス メタデータの読み取り
ms.assetid: 402de9de-8bfe-4cc2-9b8e-06e0ad925eb1
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: cc45f14f2858c551c6393510d18bcd28bac3bb6f
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223562"
---
# <a name="reading-device-metadata"></a>デバイス メタデータの読み取り

Web サービススキャナーの WIA ミニドライバーは、実行時に次のデバイスメタデータプロパティを読み取る必要があります。

**PKEY \_ pnpx \_ ServiceId**

このプロパティは、 [**wia \_ DPS \_ SERVICE \_ ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-service-id)の wia プロパティを初期化するために必要です。

**PKEY \_ pnpx \_ globalidentity**

このプロパティは、 [**wia \_ DPS \_ グローバル \_ id**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-global-identity)の wia プロパティを初期化します。

**PKEY \_ PNPX \_ ID**

このプロパティは、 [**WIA \_ DPS \_ デバイス \_ ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-device-id)デバイスプロパティを初期化します。

> [!NOTE]
> IGetMyDevicePortName を使用して直接または間接的にアクセスし[**ます。**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)

ミニドライバーは、次のような他のプロパティも読み取ることができます。

**PKEY \_ PNPX \_ ファームウェア \_ バージョン**

このプロパティは、 [**wia の \_ DPA \_ ファームウェア \_ バージョン**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-firmware-version)の wia プロパティを初期化します。

> [!NOTE]
> *WSDScan*を使用するミニドライバーは、 [**Istidevicecontrol:: GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname); を呼び出して、pnpx ID 値を取得することもできます。返されるデバイスパスは、現在の PKEY \_ pnpx \_ ID です。

これらの PKEY pnpx Xxx プロパティの詳細については、 \_ \_ *Xxx* 「 [pnp-x 実装ガイド](https://go.microsoft.com/fwlink/p/?linkid=242570)」を参照してください。

次のコード例は、前のセクションで説明したように取得された現在の関数インスタンスオブジェクトのプロパティストアを開き、ストアからデバイスプロパティを読み取る方法を示しています。

[プロパティ ストアを開くためのコード例](code-example-for-opening-a-property-store.md)

[デバイス プロパティを読み取るためのコード例](code-example-for-reading-device-properties.md)

[デバイス プロパティを初期化するためのコード例](code-example-for-initializing-device-properties.md)
