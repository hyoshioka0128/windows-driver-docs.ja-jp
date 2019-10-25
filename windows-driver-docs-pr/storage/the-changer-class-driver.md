---
title: チェンジャー クラス ドライバー
description: チェンジャー クラス ドライバー
ms.assetid: c1c2330c-9cfc-432f-945c-630dc16aa54d
keywords:
- チェンジャードライバー WDK storage、クラスドライバー
- storage チェンジャードライバー WDK、クラスドライバー
- クラスドライバー WDK storage、チェンジャードライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7edc2190dc5c0ef72b464c4f0d2251f376059c2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844447"
---
# <a name="the-changer-class-driver"></a>チェンジャー クラス ドライバー


## <span id="ddk_the_changer_class_driver_kg"></span><span id="DDK_THE_CHANGER_CLASS_DRIVER_KG"></span>


チェンジャークラスドライバーは、ハードウェアベンダーによって提供されるチェンジャー miniclass ドライバーに対して、オペレーティングシステム固有のデバイスに依存しないサービスを実行します。 チェンジャー miniclass ドライバーの詳細については、[ベンダーから提供](vendor-supplied-changer-drivers.md)されているチェンジャードライバーに関する説明を参照してください。

チェンジャークラスドライバー:

-   Miniclass ドライバーがプールメモリの割り当てと解放を行うために呼び出すメモリ割り当てルーチンを提供します。

-   Windows XP 以降のオペレーティングシステムで、オペレーティングシステムに依存しない、同期 SRBs をポートドライバーに送信する方法を提供します (Windows の相違点の説明については、「[チェンジャークラスドライバーのバージョンの違い](differences-in-changer-class-driver-versions.md)」を参照してください)。2000および Windows XP)。

-   クラス/miniclass ドライバーペアの初期化に役立ちます。

-   **チェンジャー * * * Xxx* miniclass ドライバールーチンを呼び出して、デバイス固有の情報に割り当てる領域の量を決定し、他の要求を受信するようにチェンジャーを準備します。

-   [**IRP\_\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)のデバイスに依存しないプリプロセスを実行し、デバイス\_制御要求を実行し、適切な **チェンジャー * * * Xxx* miniclass ルーチンを呼び出して、要求を完了します。

-   デバイスに依存しないプリプロセスを実行してエラーを処理し、デバイス固有の処理のために miniclass ドライバーの[**Changererror**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changererror)ルーチンを呼び出します。

-   **チェンジャー * * * Xxx* miniclass ドライバールーチンを呼び出して、製品データを取得したり、要素の状態を変更したり、クエリまたはボリュームタグのデータを照会したりします。

 

 




