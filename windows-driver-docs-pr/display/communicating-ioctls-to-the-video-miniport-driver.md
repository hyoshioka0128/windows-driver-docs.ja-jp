---
title: ビデオのミニポート ドライバーに Ioctl との通信
description: ビデオのミニポート ドライバーに Ioctl との通信
ms.assetid: 9f9ad20e-d8cf-485d-adad-c04eeb40b705
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、Ioctl
- Ioctl WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2069d020a909c5a40f055b404fc87961b11fadb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531806"
---
# <a name="communicating-ioctls-to-the-video-miniport-driver"></a>ビデオのミニポート ドライバーに Ioctl との通信


## <span id="ddk_communicating_ioctls_to_the_video_miniport_driver_gg"></span><span id="DDK_COMMUNICATING_IOCTLS_TO_THE_VIDEO_MINIPORT_DRIVER_GG"></span>


次の図は、ディスプレイ ドライバーが Ioctl を使用してビデオのミニポート ドライバーと通信する方法を示します。

![ディスプレイ ドライバー/ビデオのミニポート ドライバーの通信を示す図](images/dpy2.png)

ディスプレイ ドライバー呼び出し[ **EngDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff564838) IOCTL、ビデオのミニポート ドライバーを同期要求を送信するとします。 GDI では、入力と出力の両方に 1 つのバッファーを使用して、I/O サブシステムに要求を渡します。 I/O サブシステムは、ビデオのポートは、ビデオのミニポート ドライバーを使用した要求を処理する要求をルーティングします。

一部の IOCTL 要求がビデオのレジスタにアクセスするミニポート ドライバーを必要とし、他のユーザー ストアまたはミニポート ドライバーのデータ構造から情報を取得します。 一般に、要求には、実際の描画操作を実行するビデオのミニポート ドライバーは必要ありません。

一般に、ディスプレイ ドライバーが描画、およびその他の時間が重要な操作を処理しない限り、それ以外の場合モジュール性を決定する。 タイム クリティカルな機能を実行するミニポート ドライバーに IOCTL を送信すると、システムのパフォーマンスが低下します。

参照してください[ビデオのミニポート ドライバー I/O 制御コード](https://msdn.microsoft.com/library/windows/hardware/ff570515)ビデオ Ioctl のシステム定義の説明についてはします。 追加することで、ディスプレイ ドライバーとビデオのミニポート ドライバーの間のインターフェイスを拡張することができます、*プライベート IOCTL*、」の説明に従っては書式設定する必要があります[I/O 制御コードを定義する](https://msdn.microsoft.com/library/windows/hardware/ff543023)します。 新しい IOCTL を記述する必要がある場合は、Microsoft テクニカル サポートを最初に問い合わせてください。

 

 





