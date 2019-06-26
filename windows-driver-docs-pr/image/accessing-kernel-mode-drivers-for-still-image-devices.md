---
title: 静止画像デバイス用のカーネル モード ドライバーへのアクセス
description: 静止画像デバイス用のカーネル モード ドライバーへのアクセス
ms.assetid: f9216d3c-4930-4c26-8eac-6ee500b038e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4db5e704c0f1ecb28ad585b705af2c9975452296
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375954"
---
# <a name="accessing-kernel-mode-drivers-for-still-image-devices"></a>静止画像デバイス用のカーネル モード ドライバーへのアクセス





Microsoft では、まだ SCSI、USB バスに接続されているイメージのデバイスをサポートするために WDM ベースのカーネル モード ドライバーを提供します。 両方のドライバーがプラグ アンド プレイ デバイスをサポートし、追加、削除、開始、停止、およびプラグ アンド プレイ デバイスのレジストリ エントリを作成するためのサービスを提供します。 さらに、両方のドライバーが中断し、電源管理をサポートするデバイスの操作の再開を提供します。

ユーザー モード静止画像ミニドライバーはこれらのカーネル モード ドライバーを呼び出すことによってアクセスできる[ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**と[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (Microsoft Windows SDK のドキュメントで説明)。 **ReadFile**と**WriteFile**ブロック データ転送に使用されます。 具体的には、 **ReadFile**イメージ データを取得するために呼び出されると**WriteFile**データ ストリームとしてのコマンドを使用してデバイスにコマンドを送信するために使用します。

呼び出しの前に**ReadFile**、 **Writefile**または[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)、呼び出す必要があります、ミニドライバー [ **IStiDeviceControl::GetMyDevicePortName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)デバイスのポートの名前を取得し、そのポートの名前へのパラメーターとして[ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)します。

[SCSI ドライバー](scsi-driver.md)

[USB ドライバー](usb-driver.md)

 

 




