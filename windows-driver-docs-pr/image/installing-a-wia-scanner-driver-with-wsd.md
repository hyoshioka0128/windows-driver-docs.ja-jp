---
title: WIA スキャナー ドライバーと WSD のインストール
description: WIA スキャナー ドライバーと WSD のインストール
ms.assetid: 7dc125cb-0f20-4d3d-8124-df556a9644d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c64079f3ca14aae688e9cb02cffed6b3aba7de1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326068"
---
# <a name="installing-a-wia-scanner-driver-with-wsd"></a>WIA スキャナー ドライバーと WSD のインストール


使用する必要がありますで WSD を WIA スキャナーのドライバーをインストールする、 *WSDScan.sys*カーネル モード ドライバーは、Windows Vista の一部として提供されます。 IRP の中に\_MN\_開始\_デバイス、 *WSDScan.sys*鍵を読み取ります\_PNPX\_デバイス プロパティの ID レジストリに保存します。 デバイス プロパティ、イメージング デバイスにインストールされるために、レジストリで作成したデバイス キーに書き込まれて、 **CreateFileName** WIA レジストリ値 (に記載されている[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)). この値は、WIA ミニドライバーに WIA サービスによって返されるときに、 [ **IStiDeviceControl::GetMyDevicePortName** ](https://msdn.microsoft.com/library/windows/hardware/ff542944)呼び出し中に、 [ **IStiUSD::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff543824)メソッド。

使用している web サービス スキャナーの WIA ミニドライバー *WSDScan.sys*がその**CreateFileName**値は、デバイスがインストールされているときに初期化します。 この値を初期化するために、WIA ミニドライバーの INF ファイルを参照する必要があります**STI します。WSDSection**と**STI します。WSDSection.Services**から、 *Sti.inf*ファイル、**インストール**と**サービス**で示すように、ミニドライバーINFファイルのセクションでは[サンプルでは、Web サービス スキャナーを INF ファイル](sample-inf-file-for-a-web-services-scanner.md)します。

 

 




