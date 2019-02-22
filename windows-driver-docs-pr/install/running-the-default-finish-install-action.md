---
title: 既定の 完了-インストール アクションを実行しています。
description: 既定の 完了-インストール アクションを実行しています。
ms.assetid: a66d418e-9a66-4c11-854d-6e597ffa01f7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e30028e3f394b7bb508846638e905a9ef3a91bb0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532753"
---
# <a name="running-the-default-finish-install-action"></a>既定の 完了-インストール アクションを実行しています。


Windows 7 で、既定の 完了-インストール アクションが、システムが提供によって提供される[ **SetupDiFinishInstallAction** ](https://msdn.microsoft.com/library/windows/hardware/ff551022)関数。

デバイスには、クラスのインストーラーはありませんまたは、クラスのインストーラーがへの応答で ERROR_DI_DO_DEFAULT を返す場合、 [ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)要求と、Windows の呼び出し **。SetupDiFinishInstallAction**デバイスのすべてのインストーラーが、[完了-インストール操作を完了後します。

Windows 8 およびそれ以降のバージョンでは、完了-インストールの既定の操作はありません。

 

 





