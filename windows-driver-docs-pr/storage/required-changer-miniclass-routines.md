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
ms.openlocfilehash: 92d8658dc896b852bb854f887cd0112ed5613852
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580812"
---
# <a name="required-changer-miniclass-routines"></a>必須のチェンジャー ミニクラス ルーチン


## <span id="ddk_required_changer_miniclass_routines_kg"></span><span id="DDK_REQUIRED_CHANGER_MINICLASS_ROUTINES_KG"></span>


チェンジャー miniclass ドライバーには、次のルーチンはチェンジャー クラス ドライバーによって呼び出される必要があります。

-   **DriverEntry** --Windows XP 以降オペレーティング システムで、チェンジャー miniclass ドライバーの**DriverEntry**ルーチンの呼び出し、チェンジャー クラス ドライバーの[ **ChangerClassInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff551413)ルーチン ドライバーを初期化します。 参照してください[チェンジャー クラス ドライバーのバージョンの違い](differences-in-changer-class-driver-versions.md)詳細についてはします。 チェンジャー miniclass ドライバーがない、 **DriverEntry** Windows 2000 で日常的な。

-   [**ChangerAdditionalExtensionSize** ](https://msdn.microsoft.com/library/windows/hardware/ff551400) miniclass ドライバーでデバイス固有の情報、チェンジャーのデバイスの拡張機能で必要な追加の領域のサイズをバイト数を示します。

-   [**ChangerInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff551431)他の要求を受信するチェンジャーを準備します。

-   [**ChangerError** ](https://msdn.microsoft.com/library/windows/hardware/ff551418)チェンジャー クラス ドライバーが、デバイス非依存のエラー処理を実行した後にデバイスに固有のエラーが処理を実行します。

-   [**ChangerExchangeMedium** ](https://msdn.microsoft.com/library/windows/hardware/ff551421)と[ **ChangerMoveMedium** ](https://msdn.microsoft.com/library/windows/hardware/ff551436)メディア チェンジャー内の要素間で移動します。

-   [**ChangerReinitializeUnit**](https://msdn.microsoft.com/library/windows/hardware/ff551443)、 [ **ChangerSetAccess**](https://msdn.microsoft.com/library/windows/hardware/ff551447)、および[ **ChangerSetPosition** ](https://msdn.microsoft.com/library/windows/hardware/ff551449)位置要素とそれらへのアクセスを制御します。

-   [**ChangerGetElementStatus**](https://msdn.microsoft.com/library/windows/hardware/ff551424)、 [ **ChangerGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff551425)、 [ **ChangerGetProductData**](https://msdn.microsoft.com/library/windows/hardware/ff551427)、[ **ChangerGetStatus**](https://msdn.microsoft.com/library/windows/hardware/ff551429)、 [ **ChangerInitializeElementStatus**](https://msdn.microsoft.com/library/windows/hardware/ff551433)、および[ **ChangerQueryVolumeTags** ](https://msdn.microsoft.com/library/windows/hardware/ff551440)を取得しの場合**ChangerQueryVolumeTags**、さまざまな種類の情報を設定します。

チェンジャー miniclass ドライバー ルーチンを適切なコマンドは、記述子ブロック (CDB) コマンドを SCSI 要求のブロック (SRB) をビルドして、される Srb のシステム ポートのドライバーに送信します。

状態が返されるように、そのドライバーが、ルーチンを実装する必要がありますチェンジャーが指定したルーチンが含まれる機能をサポートしていない場合\_無効な\_デバイス\_を要求します。

必須の詳細については **チェンジャー * * * Xxx*チェンジャー miniclass ドライバーでは、ルーチンを参照してください[チェンジャー Miniclass ドライバー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff551472)します。 デバイスに対する制御要求のチェンジャーに固有の I/O 制御コードの詳細については、[チェンジャー I/O 制御コード](https://msdn.microsoft.com/library/windows/hardware/ff551469)を参照してください。

 

 




