---
title: 転送のコンテキスト
description: 転送のコンテキスト
ms.assetid: b4eadccd-afb6-4cb5-bf52-704f64d45e40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c039a325437cb72fc794bb39a3bf7738b9f9d9ff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358227"
---
# <a name="transfer-contexts"></a>転送のコンテキスト





転送コンテキストとは、ミニドライバーからアプリケーションへのデータ転送について説明する情報のコレクションです。 転送に関する情報が格納されている、 [ **MINIDRV\_転送\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)構造体。 転送のコンテキストには転送するイメージに関する情報が含まれているメンバーが含まれています。 そのサイズ、解像度、色深度 (ピクセルあたりのバイト数)、圧縮、およびイメージ形式の種類。 呼び出す前に、WIA サービスが WIA アイテムの関連するプロパティからこれらの値を取得、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッド。 値が、MINIDRV で格納し、\_転送\_CONTEXT 構造体、使いやすいアクセス用のドライバーに渡されるとします。 このプロセスでは、アプリケーションのアイテムのコンテキスト (つまり、WIA サービス コンテキスト) からこれらの値を読み取る、WIA サービス ライブラリのルーチンを使用するドライバーの必要があります。

転送のコンテキストには、転送の種類に関する情報も含まれています: ファイルのデータ転送とメモリ コールバック転送であるか。 ファイル データの転送が書き込まれるファイルへのハンドルには 1 つのメンバーが含まれます。 ミニドライバーが、このハンドルのタッチをいないことをお勧めします。 WIA サービスでは、転送が発生し、転送の完了時に終了する前に、ハンドルが表示されます。 メモリ コールバックのデータ転送 (および場合、アプリケーションは、ミニドライバーから更新プログラムを受信するには、ファイルのデータ転送)、メンバーには、ミニドライバーのコールバック ルーチンのアドレスが含まれています。

他のメンバーはすべて、転送に使用されるバッファーの合計サイズなどの情報を含めることが、ミニドライバーまたは WIA サービス割り当てにかどうかとします。 参照してください[ **MINIDRV\_転送\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)この構造体のメンバーの完全な一覧についてはします。

ミニドライバー、と共に、 [ **wiasGetImageInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetimageinformation)関数を転送の多く (ピクセル単位) と、行の数で幅など、イメージを説明するコンテキスト項目を設定します。 WIA サービスのセットが (必要な場合) 多くのファイルなどのデータ転送を懸念する転送コンテキスト項目の処理、転送の種類。

 

 




