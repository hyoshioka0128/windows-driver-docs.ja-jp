---
title: 記憶域クラス ドライバーの一般的な機能
description: 記憶域クラス ドライバーの一般的な機能
ms.assetid: 4fc92d20-5570-4680-bc7b-f6e84524a672
keywords:
- 記憶域クラス ドライバー WDK、機能
- クラス ドライバー WDK ストレージの機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8669a4124f033dad43947321fc7d17ad62b2a533
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579121"
---
# <a name="storage-class-drivers-general-functionality"></a>記憶域クラス ドライバーの一般的な機能


## <span id="ddk_storage_class_drivers_general_functionality_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GENERAL_FUNCTIONALITY_KG"></span>


記憶域のポート ドライバーには、ストレージ クラス ドライバーは、組み込み、デバイスの種類に固有の機能を備えたより高度なドライバーです。 一般に、すべての記憶域クラス ドライバーは、次の担当です。

-   渡されると主張して各デバイスを物理デバイス オブジェクト (PDO) によって表される、 *AddDevice* PnP マネージャーによってルーチン

-   各このような PDO (FDO) 機能のデバイス オブジェクトを作成して、デバイス スタックへの追加

-   物理デバイス オブジェクト (Pdo) を表す各パーティションを作成して、列挙型への応答を要求、ドライバーは、分割可能なデバイスを制御する場合

-   システムの I/O 要求 (Irp) の解釈

-   SCSI ポート クラス/インターフェイス要求 (SCSI Cdb でされる Srb) への Irp のマッピング

-   要求のタイムアウト値を確立します。

-   基になる HBA の制限に合わせてデータ転送のサイズの制限

-   条件の確認の状態またはバスのリセットなど、記憶域ポート ドライバーによって処理されていないエラー状態の処理

 

 




