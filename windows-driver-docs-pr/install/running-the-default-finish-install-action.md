---
title: 既定のインストールの完了アクションの実行
description: 既定のインストールの完了アクションの実行
ms.assetid: a66d418e-9a66-4c11-854d-6e597ffa01f7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c8e8632430e9d1c261a9636469d9899189be04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378034"
---
# <a name="running-the-default-finish-install-action"></a>既定のインストールの完了アクションの実行


Windows 7 で、既定の 完了-インストール アクションが、システムが提供によって提供される[ **SetupDiFinishInstallAction** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))関数。

デバイスには、クラスのインストーラーはありませんまたは、クラスのインストーラーがへの応答で ERROR_DI_DO_DEFAULT を返す場合、 [ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)要求と、Windows の呼び出し **。SetupDiFinishInstallAction**デバイスのすべてのインストーラーが、完了-インストール操作を完了後します。

Windows 8 およびそれ以降のバージョンでは、完了-インストールの既定の操作はありません。

 

 





