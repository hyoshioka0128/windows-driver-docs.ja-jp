---
title: 静止画像デバイス用のカーネル モード ドライバーへのアクセス
description: 静止画像デバイス用のカーネル モード ドライバーへのアクセス
ms.assetid: f9216d3c-4930-4c26-8eac-6ee500b038e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ae8d4ced83e66e002c6007f339fecf72614001
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840916"
---
# <a name="accessing-kernel-mode-drivers-for-still-image-devices"></a>静止画像デバイス用のカーネル モード ドライバーへのアクセス





Microsoft では、SCSI および USB バスに接続された静止イメージデバイスをサポートするために、WDM ベースのカーネルモードドライバーを提供しています。 どちらのドライバーもプラグアンドプレイデバイスをサポートし、プラグアンドプレイデバイスのレジストリエントリを追加、削除、開始、停止、および作成するためのサービスを提供します。 また、どちらのドライバーも、電源管理をサポートするデバイスの中断と再開の操作を提供します。

ユーザーモード静止画像ミニドライバーは、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**、および[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出すことによって、これらのカーネルモードドライバーにアクセスできます (Microsoft Windows SDK のドキュメントを参照)。 **ReadFile**と**WriteFile**は、データの転送をブロックするために使用されます。 具体的には、 **ReadFile**はイメージデータを取得するために呼び出され、 **WriteFile**は、データストリームとしてコマンドを受け取るデバイスにコマンドを送信するために使用されます。

**ReadFile**、 **Writefile** 、または[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出す前に、ミニドライバーは[**istidevicecontrol:: GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)を呼び出してデバイスのポート名を取得し、そのポート名を[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)のパラメーターとして使用する必要があります。

[SCSI ドライバー](scsi-driver.md)

[USB ドライバー](usb-driver.md)

 

 




