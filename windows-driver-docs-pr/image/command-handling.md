---
title: コマンドの処理
description: コマンドの処理
ms.assetid: 1b940585-8228-4857-92bf-c77c789f6ad5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d32b3cef55e0cbb53d715e2f0b8291987f1df60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840870"
---
# <a name="command-handling"></a>コマンドの処理





Wia アーキテクチャを使用すると、wia アプリケーションで特定のコマンドを WIA ミニドライバーに送信できます。 このコマンドは、WIA 項目ツリーのルート項目にのみ送信できます。 (ミニドライバーによって、機能テーブルでサポートされているすべてのコマンドが報告されることに注意してください)。

WIA アプリケーションによって発行されたコマンドは、WIA ミニドライバーに直接アクセスしません。 代わりに、アプリケーションはコマンドを WIA サービスに送信します。 次に、WIA サービスがこのコマンドを WIA ミニドライバーに転送します。 ミニドライバーがコマンドを受け取ると ( [**IWiaMiniDrv::D rvdevicecommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)メソッドのパラメーターとして)、ミニドライバーはコマンドを満たすためにデバイスにアクセスする必要がある場合があります。

場合によっては、コマンドで新しい子ドライバ項目を作成するためにミニドライバーが必要になることがあります。 たとえば、デジタル静止カメラデバイスでは、[**画像**の表示] コマンドがサポートされている場合があります。 ミニドライバーがこのコマンドを受け取ると、カメラに画像を撮影するように指示します。 カメラが画像の撮影要求を実行すると、カメラはそのメディアに新しいイメージを作成し、WIA ミニドライバーはその項目ツリーに新しいドライバー項目を追加します。

 

 




