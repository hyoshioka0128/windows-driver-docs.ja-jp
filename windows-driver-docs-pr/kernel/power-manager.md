---
title: 電源マネージャー
description: 電源マネージャー
ms.assetid: f7727368-6edd-427b-9fb3-02f80538807b
keywords:
- 電源マネージャー WDK カーネル
- 使用状況マネージャー WDK の電源管理
- 電源 Irp WDK カーネルでは、電源マネージャー
- システム全体の電源ポリシー WDK カーネル
- 電源ポリシー WDK カーネル
- スリープの電源管理の WDK カーネル
- 休止状態の電源管理の WDK カーネル
- シャット ダウンの電源管理の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8831d9c30c160b29283445174709ba90125e8869
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374193"
---
# <a name="power-manager"></a>電源マネージャー





電源マネージャーは、システムの電力使用状況を管理する責任を負います。 システム全体の電源ポリシーを管理し、システムを通じて power Irp のパスを追跡します。

電源マネージャーでは、電源操作を要求を送信して[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)ドライバーへの要求。 要求は、新しい電源状態を指定できます。 または電源状態の変更が可能かどうかを問い合わせることができます。

電源マネージャーが送信することによって適切な電源操作を要求するスリープ、休止状態またはシャット ダウンが必要な場合、 **IRP\_MJ\_POWER**デバイス ツリー内の各リーフ ノードに要求します。 電源マネージャー、システムをスリープするかどうかを決定するでは、次は、休止状態またはシャット ダウンを検討します。

-   システム アクティビティのレベル

-   システムのバッテリ レベル

-   シャット ダウン、休止状態、またはアプリケーションからの要求をスリープ状態

-   [電源] ボタンを押すなどのユーザー操作

-   コントロール パネルの設定

詳細については、次を参照してください。 [Windows カーネル モードの電源マネージャー](windows-kernel-mode-power-manager.md)します。

 

 




