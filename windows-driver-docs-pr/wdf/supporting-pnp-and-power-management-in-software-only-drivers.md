---
title: ソフトウェア専用ドライバーでの PnP と電源管理のサポート
description: ソフトウェア専用ドライバーでの PnP と電源管理のサポート
ms.assetid: bcfca8b2-68d6-4875-8687-27351becd6f4
keywords:
- PnP WDK KMDF、ソフトウェアのみのドライバー
- プラグ アンド プレイ WDK KMDF、ソフトウェアのみのドライバー
- 電源管理 WDK KMDF、ソフトウェアのみのドライバー
- ソフトウェア専用のドライバー WDK KMDF
- フィルター ドライバー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11c5c3ab8e70a07edb3b1e15ced92067f6851cd5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368054"
---
# <a name="supporting-pnp-and-power-management-in-software-only-drivers"></a>ソフトウェア専用ドライバーでの PnP と電源管理のサポート


*ソフトウェア専用のドライバー*ドライバーは、ハードウェアにアクセスしません。 一部のソフトウェア専用のドライバーは、ハードウェアにアクセスしないドライバー スタック内に存在します。 これらのドライバーはハードウェアにアクセスしないため、通常がない PnP または電源管理操作を実行します。

その他のソフトウェア専用のドライバーは、フィルター: ハードウェアへのアクセスはドライバーのスタック内に存在するが、フィルター ドライバーはハードウェアにアクセスできません。 フィルター ドライバー、PnP を指定する I/O 要求を受信した場合、または電源管理操作、ドライバー通常だけに要求を渡します次のドライバーです。 フレームワークは、これらの要求のインターセプトを framework ベースのドライバーが要求を確認しないように、渡します。

ソフトウェア専用ドライバーでは、ドライバーを記述するかどうかは[デバイス オブジェクトを作成します。](creating-a-framework-device-object.md)が通常は必要ありません PnP または電源管理イベントを処理するコールバック関数のすべてのイベントを提供します。 ドライバーで使用する場合[framework キュー オブジェクト](framework-queue-objects.md)、設定する必要があります、 **PowerManaged**のキューのメンバー [ **WDF\_IO\_キュー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_config)構造体を**WdfFalse**または**WdfUseDefault**します。

いくつかのソフトウェア専用のドライバーを[関数ドライバー](supporting-pnp-and-power-management-in-function-drivers.md)します。 つまり、1 つのドライバーは可能性があります、ハードウェアにアクセスしない仮想デバイスをサポートするソフトウェア専用のドライバーとハードウェア デバイスをサポートする機能のドライバーとして機能します。

 

 





