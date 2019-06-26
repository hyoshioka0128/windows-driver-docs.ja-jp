---
title: 必須のチェンジャー ミニクラス ルーチン
description: 必須のチェンジャー ミニクラス ルーチン
ms.assetid: bd706c00-5f6b-4bda-b6a1-a61046303e12
keywords:
- チェンジャー ドライバー WDK ストレージ、miniclass ドライバー
- 記憶域チェンジャー ドライバー WDK、miniclass ドライバー
- miniclass ドライバー WDK チェンジャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b180062444034fadf24cc4889cd4d536f4cec36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356643"
---
# <a name="required-changer-miniclass-routines"></a>必須のチェンジャー ミニクラス ルーチン


## <span id="ddk_required_changer_miniclass_routines_kg"></span><span id="DDK_REQUIRED_CHANGER_MINICLASS_ROUTINES_KG"></span>


チェンジャー miniclass ドライバーには、次のルーチンはチェンジャー クラス ドライバーによって呼び出される必要があります。

-   **DriverEntry** --Windows XP 以降オペレーティング システムで、チェンジャー miniclass ドライバーの**DriverEntry**ルーチンの呼び出し、チェンジャー クラス ドライバーの[ **ChangerClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerclassinitialize)ルーチン ドライバーを初期化します。 参照してください[チェンジャー クラス ドライバーのバージョンの違い](differences-in-changer-class-driver-versions.md)詳細についてはします。 チェンジャー miniclass ドライバーがない、 **DriverEntry** Windows 2000 で日常的な。

-   [**ChangerAdditionalExtensionSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changeradditionalextensionsize) miniclass ドライバーでデバイス固有の情報、チェンジャーのデバイスの拡張機能で必要な追加の領域のサイズをバイト数を示します。

-   [**ChangerInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerinitialize)他の要求を受信するチェンジャーを準備します。

-   [**ChangerError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changererror)チェンジャー クラス ドライバーが、デバイス非依存のエラー処理を実行した後にデバイスに固有のエラーが処理を実行します。

-   [**ChangerExchangeMedium** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerexchangemedium)と[ **ChangerMoveMedium** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changermovemedium)メディア チェンジャー内の要素間で移動します。

-   [**ChangerReinitializeUnit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerreinitializeunit)、 [ **ChangerSetAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changersetaccess)、および[ **ChangerSetPosition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changersetposition)位置要素とそれらへのアクセスを制御します。

-   [**ChangerGetElementStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changergetelementstatus)、 [ **ChangerGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changergetparameters)、 [ **ChangerGetProductData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changergetproductdata)、[ **ChangerGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changergetstatus)、 [ **ChangerInitializeElementStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerinitializeelementstatus)、および[ **ChangerQueryVolumeTags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerqueryvolumetags)を取得しの場合**ChangerQueryVolumeTags**、さまざまな種類の情報を設定します。

チェンジャー miniclass ドライバー ルーチンを適切なコマンドは、記述子ブロック (CDB) コマンドを SCSI 要求のブロック (SRB) をビルドして、される Srb のシステム ポートのドライバーに送信します。

状態が返されるように、そのドライバーが、ルーチンを実装する必要がありますチェンジャーが指定したルーチンが含まれる機能をサポートしていない場合\_無効な\_デバイス\_を要求します。

必須の詳細については **チェンジャー * * * Xxx*チェンジャー miniclass ドライバーでは、ルーチンを参照してください[チェンジャー Miniclass ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 デバイスに対する制御要求のチェンジャーに固有の I/O 制御コードの詳細については、次を参照してください。[チェンジャー I/O 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 




