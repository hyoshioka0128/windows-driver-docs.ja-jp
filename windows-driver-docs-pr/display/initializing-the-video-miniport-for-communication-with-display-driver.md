---
title: ビデオミニポート/ディスプレイドライバーの通信を初期化しています
description: ディスプレイドライバーとの通信用にビデオミニポートを初期化しています
ms.assetid: 73ba423c-7ebc-4a07-aed0-d2e33f11b878
keywords:
- ビデオミニポートドライバー WDK Windows 2000、初期化
- ビデオミニポートドライバーの初期化
- HwVidInitialize
- ワンタイム初期化 WDK ビデオミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 90e4cd58ebd5016b17b406b70f1a52b7438cd316
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840369"
---
# <a name="initializing-the-video-miniport-for-communication-with-display-driver"></a>ディスプレイドライバーとの通信用にビデオミニポートを初期化しています

PnP マネージャーによって検出され、ミニポートドライバーによって正常に構成されたアダプターごとに、対応するディスプレイドライバーが読み込まれると、ミニポートドライバーの[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)関数が呼び出されます。 *HwVidInitialize*は、ソフトウェアの状態情報を初期化できますが、アダプターに表示される状態を設定することはできません。 *HwVidInitialize*から戻る場合、アダプターはミニポートドライバーの[*HwVidResetHw*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_reset_hw)ルーチンから返されたときと同じ状態に設定する必要があります。 *HwVidResetHw*の詳細については、「[ビデオミニポートドライバーでアダプターをリセットする](resetting-the-adapter-in-video-miniport-drivers.md)」を参照してください。

必要に応じて、ミニポートドライバーの*HwVidInitialize*関数は、 *HwVidFindAdapter*関数によって延期されたアダプターに対して1回限りの初期化操作を実行できます。 たとえば、ミニポートドライバーは、アダプターへのマイクロコードの読み込みを延期し、 *HwVidInitialize*関数が[**VideoPortGetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetregistryparameters)を呼び出すことがあります。

*HwVidInitialize*の場合。 詳細については、「[ビデオ要求の処理 (Windows 2000 モデル)](processing-video-requests--windows-2000-model-.md) 」を参照してください。

通常、ディスプレイドライバーは、エンドユーザーに表示されるディスプレイを制御します。ただし、NT ベースのオペレーティングシステムを実行している x86 ベースのコンピューターで全画面表示の MS-DOS アプリケーションを実行する場合はまれです。 この機能を VGA 互換のミニポートドライバーでサポートする方法の詳細については、「 [Vga 互換ビデオミニポートドライバー (Windows 2000 モデル)](vga-compatible-video-miniport-drivers--windows-2000-model-.md)」を参照してください。

[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)関数は、 [**VideoPortGetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetregistryparameters)または[**VideoPortSetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsetregistryparameters)を呼び出して、レジストリ内の構成情報を取得および設定できます。 たとえば、 *HwVidInitialize*は**VideoPortSetRegistryParameters**を呼び出して、次回の起動時にレジストリに不揮発性構成情報を設定する場合があります。 インストールプログラムによってレジストリに書き込まれる、アダプター固有のバス相対構成パラメーターを取得するために、 **VideoPortGetRegistryParameters**を呼び出す場合があります。

 

 





