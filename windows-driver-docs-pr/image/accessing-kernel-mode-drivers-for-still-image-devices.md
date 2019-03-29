---
title: 静止画像デバイス用のカーネル モード ドライバーへのアクセス
description: 静止画像デバイス用のカーネル モード ドライバーへのアクセス
ms.assetid: f9216d3c-4930-4c26-8eac-6ee500b038e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa0ffce7def107a1e63677b607513abd868100fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577654"
---
# <a name="accessing-kernel-mode-drivers-for-still-image-devices"></a>静止画像デバイス用のカーネル モード ドライバーへのアクセス





Microsoft では、まだ SCSI、USB バスに接続されているイメージのデバイスをサポートするために WDM ベースのカーネル モード ドライバーを提供します。 両方のドライバーがプラグ アンド プレイ デバイスをサポートし、追加、削除、開始、停止、およびプラグ アンド プレイ デバイスのレジストリ エントリを作成するためのサービスを提供します。 さらに、両方のドライバーが中断し、電源管理をサポートするデバイスの操作の再開を提供します。

ユーザー モード静止画像ミニドライバーはこれらのカーネル モード ドライバーを呼び出すことによってアクセスできる[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)、 **ReadFile**、 **WriteFile**と[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) (Microsoft Windows SDK のドキュメントで説明)。 **ReadFile**と**WriteFile**ブロック データ転送に使用されます。 具体的には、 **ReadFile**イメージ データを取得するために呼び出されると**WriteFile**データ ストリームとしてのコマンドを使用してデバイスにコマンドを送信するために使用します。

呼び出しの前に**ReadFile**、 **Writefile**または[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)、呼び出す必要があります、ミニドライバー [ **IStiDeviceControl::GetMyDevicePortName** ](https://msdn.microsoft.com/library/windows/hardware/ff542944)デバイスのポートの名前を取得し、そのポートの名前へのパラメーターとして[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)します。

[SCSI ドライバー](scsi-driver.md)

[USB ドライバー](usb-driver.md)

 

 




