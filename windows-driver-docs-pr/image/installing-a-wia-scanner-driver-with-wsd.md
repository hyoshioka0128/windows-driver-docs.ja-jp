---
title: WSD を使用した WIA スキャナードライバーのインストール
description: WSD を使用した WIA スキャナードライバーのインストール
ms.assetid: 7dc125cb-0f20-4d3d-8124-df556a9644d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d48352a0bbdc9b4a5eea87a7b84035d9bc901565
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840816"
---
# <a name="installing-a-wia-scanner-driver-with-wsd"></a>WSD を使用した WIA スキャナードライバーのインストール


WSD で WIA スキャナードライバーをインストールするには、Windows Vista の一部として提供されている*WSDScan*カーネルモードドライバーを使用する必要があります。 IRP\_によって\_デバイス\_開始されると、 *WSDScan*は PKEY\_pnpx\_ID デバイスプロパティを読み取り、それをレジストリに保存します。 デバイスプロパティは、インストールされているイメージングデバイス用のレジストリ内に作成されたデバイスキーと、 **Createfilename** wia レジストリ値 (「 [Wia デバイスの INF ファイル](inf-files-for-wia-devices.md)」で説明されています) に書き込まれます。 この値は、iミニドライバー [ **:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)メソッドの実行中に[**iGetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)呼び出しが行われたときに、wia サービスによって返されます。

*WSDScan*を使用する web サービススキャナーの WIA ミニドライバーの**createfilename**値は、デバイスのインストール時に初期化されます。 この値を初期化するには、WIA ミニドライバーの INF ファイルで、STI を参照する必要があり**ます。WSDSection**と**STI。** [Web サービススキャナーのサンプル inf ファイル](sample-inf-file-for-a-web-services-scanner.md)に示されているように、ミニドライバー *inf ファイルの* **Install** and **Services**セクションにある WSDSection ファイルからのサービス。

 

 




