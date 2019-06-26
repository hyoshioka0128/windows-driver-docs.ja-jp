---
title: チェンジャー クラス ドライバー
description: チェンジャー クラス ドライバー
ms.assetid: c1c2330c-9cfc-432f-945c-630dc16aa54d
keywords:
- チェンジャー ドライバー WDK ストレージ クラス ドライバー
- 記憶域チェンジャー ドライバー WDK、クラス ドライバー
- チェンジャー ドライバーのクラス ドライバー WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a335cd9dec3c85127de78dee5c7f919a1df6315b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386805"
---
# <a name="the-changer-class-driver"></a>チェンジャー クラス ドライバー


## <span id="ddk_the_changer_class_driver_kg"></span><span id="DDK_THE_CHANGER_CLASS_DRIVER_KG"></span>


チェンジャー クラス ドライバーは、ハードウェア ベンダーによって提供されるチェンジャー miniclass ドライバーの特定のオペレーティング システム、デバイスに依存しないサービスを実行します。 チェンジャー miniclass ドライバーの詳細については、次を参照してください。 [Vendor-Supplied チェンジャー ドライバー](vendor-supplied-changer-drivers.md)します。

チェンジャー クラス ドライバー:

-   メモリ プール メモリの割り当てし、解放の呼び出しを miniclass ドライバー割り当てルーチンを提供します。

-   Microsoft Windows XP 以降のオペレーティング システムでポート ドライバーに同期される Srb を送信する、オペレーティング システムに依存しない手段を提供します (を参照してください[チェンジャー クラス ドライバーのバージョンの違い](differences-in-changer-class-driver-versions.md)の詳細については、相違点と、Windows 2000 と Windows XP の間)。

-   により、クラス/miniclass ドライバーのペアを初期化します。

-   呼び出し **チェンジャー * * * Xxx* miniclass ドライバーのルーチンをデバイスに固有の情報を割り当てること、およびその他の要求を受信するチェンジャーを準備する空き領域の量を決定します。

-   デバイス非依存の前処理を実行します[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求、呼び出しの適切な **チェンジャー * * * Xxx* miniclass ルーチンでは、要求が完了するとします。

-   デバイスに依存しないはエラーの前処理を実行し、呼び出す miniclass ドライバーの[ **ChangerError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changererror)デバイスに固有の処理ルーチン。

-   呼び出し **チェンジャー * * * Xxx*製品データを取得する miniclass ドライバー ルーチンは要素の状態を変更またはクエリの照会またはボリュームのデータにタグを付けます。

 

 




