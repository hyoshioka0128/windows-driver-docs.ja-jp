---
title: WIA スキャナー ドライバーと WSD のインストール
description: WIA スキャナー ドライバーと WSD のインストール
ms.assetid: 7dc125cb-0f20-4d3d-8124-df556a9644d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc0277e287db194a6fe60ec5dc70024b49c03568
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378934"
---
# <a name="installing-a-wia-scanner-driver-with-wsd"></a>WIA スキャナー ドライバーと WSD のインストール


使用する必要がありますで WSD を WIA スキャナーのドライバーをインストールする、 *WSDScan.sys*カーネル モード ドライバーは、Windows Vista の一部として提供されます。 IRP の中に\_MN\_開始\_デバイス、 *WSDScan.sys*鍵を読み取ります\_PNPX\_デバイス プロパティの ID レジストリに保存します。 デバイス プロパティ、イメージング デバイスにインストールされるために、レジストリで作成したデバイス キーに書き込まれて、 **CreateFileName** WIA レジストリ値 (に記載されている[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)). この値は、WIA ミニドライバーに WIA サービスによって返されるときに、 [ **IStiDeviceControl::GetMyDevicePortName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)呼び出し中に、 [ **IStiUSD::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)メソッド。

使用している web サービス スキャナーの WIA ミニドライバー *WSDScan.sys*がその**CreateFileName**値は、デバイスがインストールされているときに初期化します。 この値を初期化するために、WIA ミニドライバーの INF ファイルを参照する必要があります**STI します。WSDSection**と**STI します。WSDSection.Services**から、 *Sti.inf*ファイル、**インストール**と**サービス**で示すように、ミニドライバーINFファイルのセクションでは[サンプルでは、Web サービス スキャナーを INF ファイル](sample-inf-file-for-a-web-services-scanner.md)します。

 

 




