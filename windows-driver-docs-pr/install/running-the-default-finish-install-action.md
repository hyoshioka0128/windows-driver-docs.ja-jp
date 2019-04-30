---
title: 既定のインストールの完了アクションの実行
description: 既定のインストールの完了アクションの実行
ms.assetid: a66d418e-9a66-4c11-854d-6e597ffa01f7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e30028e3f394b7bb508846638e905a9ef3a91bb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382917"
---
# <a name="running-the-default-finish-install-action"></a>既定のインストールの完了アクションの実行


Windows 7 で、既定の 完了-インストール アクションが、システムが提供によって提供される[ **SetupDiFinishInstallAction** ](https://msdn.microsoft.com/library/windows/hardware/ff551022)関数。

デバイスには、クラスのインストーラーはありませんまたは、クラスのインストーラーがへの応答で ERROR_DI_DO_DEFAULT を返す場合、 [ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)要求と、Windows の呼び出し **。SetupDiFinishInstallAction**デバイスのすべてのインストーラーが、[完了-インストール操作を完了後します。

Windows 8 およびそれ以降のバージョンでは、完了-インストールの既定の操作はありません。

 

 





