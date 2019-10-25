---
title: IOCTL とビデオ ミニポート ドライバーの通信
description: IOCTL とビデオ ミニポート ドライバーの通信
ms.assetid: 9f9ad20e-d8cf-485d-adad-c04eeb40b705
keywords:
- ビデオミニポートドライバー WDK Windows 2000、Ioctl
- Ioctl WDK Windows 2000 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d67b28e0203bbe9d30beabbd440e869ab63f4113
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839051"
---
# <a name="communicating-ioctls-to-the-video-miniport-driver"></a>IOCTL とビデオ ミニポート ドライバーの通信


## <span id="ddk_communicating_ioctls_to_the_video_miniport_driver_gg"></span><span id="DDK_COMMUNICATING_IOCTLS_TO_THE_VIDEO_MINIPORT_DRIVER_GG"></span>


次の図は、表示ドライバーが Ioctl を使用してビデオミニポートドライバーと通信する方法を示しています。

![ディスプレイドライバー/ビデオミニポートドライバーの通信を示す図](images/dpy2.png)

ディスプレイドライバーは、IOCTL を使用して[**EngDeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)を呼び出し、ビデオミニポートドライバーに同期要求を送信します。 GDI では、入力と出力の両方に1つのバッファーを使用して、i/o サブシステムに要求を渡します。 I/o サブシステムは、ビデオミニポートドライバーを使用して要求を処理するビデオポートに要求をルーティングします。

一部の IOCTL 要求では、ミニポートドライバーがビデオレジスタにアクセスしたり、ミニポートドライバーのデータ構造の情報を格納または取得したりする必要があります。 通常、ビデオミニポートドライバーが実際の描画操作を実行するために必要な要求はありません。

一般に、モジュールが特に指定しない限り、表示ドライバーは描画およびその他のタイムクリティカルな操作を処理します。 タイムクリティカルな機能を実行するために IOCTL をミニポートドライバーに送信すると、システムのパフォーマンスが低下する可能性があります。

システム定義のビデオ Ioctl の説明については、[ビデオミニポートドライバーの I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に関する記事をご覧ください。 [I/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)に関するページで説明されているように、*プライベート IOCTL*を追加することで、表示ドライバーとビデオミニポートドライバーの間のインターフェイスを拡張できます。 新しい IOCTL を作成する必要がある場合は、まず Microsoft テクニカルサポートにお問い合わせください。

 

 





