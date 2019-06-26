---
title: コマンドの処理
description: コマンドの処理
ms.assetid: 1b940585-8228-4857-92bf-c77c789f6ad5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a7df5390b327c1cc6451f4e728bda98237d16eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358643"
---
# <a name="command-handling"></a>コマンドの処理





WIA アーキテクチャ WIA アプリケーション WIA ミニドライバーに特定のコマンドを送信することができます。 このコマンドは、WIA 項目ツリーのルート項目にのみ送信できます。 (、ミニドライバーをレポートのすべてのコマンド、機能テーブルでサポートすることに注意してください)。

WIA アプリケーションによって発行されたコマンドは、WIA ミニドライバーに直接は説明しません。 代わりに、アプリケーションは、WIA サービスにコマンドを送信します。 WIA サービスは、このコマンドを WIA ミニドライバーに転送します。 ミニドライバーは、コマンドを受信すると (のパラメーターとして、 [ **IWiaMiniDrv::drvDeviceCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)メソッド) をミニドライバーは、コマンドを満たすためにデバイスにアクセスする必要があります。

場合によっては、コマンドは、新しい子ドライバー項目を作成するミニドライバーを必要があります。 たとえば、デジタル カメラ デバイスをサポート可能性があります、 **TakePicture**コマンド。 ミニドライバーは、このコマンドを受信する場合は、画像を撮影するカメラを指示します。 カメラは写真を撮るに要求を実行と、カメラは、そのメディアでは、新しいイメージを作成します WIA ミニドライバーは、その項目のツリーに新しいドライバー項目を追加します。

 

 




