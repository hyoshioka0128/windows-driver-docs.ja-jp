---
title: デバイス構成領域へのアクセス
description: デバイス構成領域へのアクセス
ms.assetid: 082500ae-9df2-4f8b-8be3-ff2b95067a12
keywords:
- デバイス構成領域、I/O の WDK カーネル
- デバイス構成領域 WDK I/O
- 構成領域 WDK I/O
- WDK の I/O の領域
- WDK の I/O のリソース情報
- ドライバー スタック WDK 構成情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f772f9bfa746221fb8295f8384a876a036e0bdd6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539711"
---
# <a name="accessing-device-configuration-space"></a>デバイス構成領域へのアクセス





いくつかのバスのバスに接続されている各デバイスの特別な構成の領域にアクセスする手段です。 このセクションでは、ドライバーはドライバー スタックは、ターゲット デバイスのドライバーと同じで機能のドライバーまたはフィルター ドライバーとして読み込まれているドライバーがターゲット デバイスの構成の領域から情報を取得する方法について説明します。

Microsoft Windows NT 4.0 では、ドライバーから情報を取得、ターゲット デバイスの構成領域、バスをスキャンし、呼び出すことによって、 [ **HalGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff546599)と[ **HalGetBusDataByOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff546606)ルーチン。 Windows 2000 および以降のオペレーティング システムでは、ハードウェア バスは、HAL しないと、それぞれのバス ドライバーによって制御されます。 そのため、ドライバーがバスに関連する情報を取得するために使用する HAL ルーチンのすべてが Windows 2000 廃止されました。

デバイスの構成領域には、デバイスとリソース要件の説明が含まれています。 Windows 2000 および以降のオペレーティング システムでは、ドライバーは、デバイス リソースを検索するクエリを実行するには必要ありません。 ドライバー マネージャーを取得、リソース、プラグ アンド プレイ (PnP) から[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 通常、適切に記述されたドライバーでは、情報が正常に機能する必要はありません。 何らかの理由では、ドライバーは、この情報を必要とする場合は、コードのサンプルで、 [IRQL でデバイスの構成情報を取得するパッシブ =\_レベル](obtaining-device-configuration-information-at-irql---passive-level.md)セクションは、リソースを取得する方法を示します。 ドライバーは、適切な PnP 要求を送信するターゲット デバイスの基になる物理デバイス オブジェクト (PDO) 必要があるために、ターゲット デバイスのドライバー スタックの一部にすることがあります。

 

 




