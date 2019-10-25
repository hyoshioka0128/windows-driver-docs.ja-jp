---
title: 必須のチェンジャー ミニクラス ルーチン
description: 必須のチェンジャー ミニクラス ルーチン
ms.assetid: bd706c00-5f6b-4bda-b6a1-a61046303e12
keywords:
- チェンジャードライバー WDK storage、miniclass drivers
- storage チェンジャードライバー WDK、miniclass ドライバー
- miniclass drivers WDK チェンジャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8d690052221b399804bb9bbecc83e1741be8715
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842694"
---
# <a name="required-changer-miniclass-routines"></a>必須のチェンジャー ミニクラス ルーチン


## <span id="ddk_required_changer_miniclass_routines_kg"></span><span id="DDK_REQUIRED_CHANGER_MINICLASS_ROUTINES_KG"></span>


チェンジャーの miniclass ドライバーには、チェンジャークラスドライバーによって呼び出される次のルーチンが必要です。

-   **Driverentry** --Windows XP 以降のオペレーティングシステムでは、チェンジャーの miniclass ドライバーの**driverentry**ルーチンがチェンジャークラスドライバーの[**changerclassinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize)ルーチンを呼び出してドライバーを初期化します。 詳細については、「[チェンジャークラスドライバーバージョンの相違点](differences-in-changer-class-driver-versions.md)」を参照してください。 チェンジャー miniclass ドライバーには、Windows 2000 に**Driverentry**ルーチンがありません。

-   [**Changeradditionalextensionsize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changeradditionalextensionsize)は、デバイス固有の情報を格納するために、チェンジャーのデバイス拡張で miniclass ドライバーが必要とする追加領域のバイト数を示します。

-   [**Changerinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerinitialize)は、他の要求を受信するようにチェンジャーを準備します。

-   [**Changererror**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changererror)は、チェンジャークラスドライバーがデバイスに依存しないエラー処理を実行した後に、デバイス固有のエラー処理を実行します。

-   [**ChangerExchangeMedium**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerexchangemedium)と[**ChangerMoveMedium**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changermovemedium)は、チェンジャー内の要素間でメディアを移動します。

-   [**Changerreinitializeunit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerreinitializeunit)、 [**changersetaccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changersetaccess)、および[**changersetposition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changersetposition)の各要素へのアクセスを制御します。

-   [**ChangerGetElementStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changergetelementstatus)、 [**changergetparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changergetparameters)、 [**changergetproductdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changergetproductdata)、 [**ChangerGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changergetstatus)、 [**changerinitializeelementstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerinitializeelementstatus)、および[**ChangerQueryVolumeTags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerqueryvolumetags) get と (の**場合)ChangerQueryVolumeTags**では、さまざまな種類のチェンジャー情報を設定します。

チェンジャー miniclass ドライバールーチンは、通常、適切なコマンドに対してコマンド記述子ブロック (CDB) を使用して SCSI 要求ブロック (SRB) を構築し、SRBs をシステムポートドライバーに送信します。

チェンジャーが特定のルーチンによって暗黙的に指定された機能をサポートしていない場合は、そのドライバーがルーチンを実装する必要があります。これにより、デバイス\_要求\_の状態\_無効になります。

チェンジャー miniclass ドライバーの必須の **チェンジャー * * * Xxx*ルーチンの詳細については、「[チェンジャー miniclass ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。 デバイスコントロール要求のチェンジャー固有の i/o 制御コードの詳細については、「[チェンジャー I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 




