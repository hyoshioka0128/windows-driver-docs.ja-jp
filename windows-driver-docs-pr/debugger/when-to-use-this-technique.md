---
title: この手法を使用する状況
description: この手法を使用する状況
ms.assetid: 40c9e2aa-35a3-4169-8305-bddc199a5c98
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9db617441839193c6421a604adadd7795f3d9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325848"
---
# <a name="when-to-use-this-technique"></a>この手法を使用する状況


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


便利なまたはにも必要ないくつかの状況がある[カーネル デバッガーからユーザー モードのデバッグを制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md):

-   または実行するユーザー モードのデバッグしますが、も必要がありますでユーザー モードのターゲットが実行されている Windows カーネルの制御のいくつかのカーネル モードのデバッグ機能を使用して、問題を分析する必要があります必要がある場合。

-   ときに、ユーザー モード ターゲットは、CSRSS または WinLogon などの Windows プロセスです。 これらのターゲットをデバッグする方法の詳細については、次を参照してください。[デバッグ CSRSS](debugging-csrss.md)と[デバッグ WinLogon](debugging-winlogon.md)します。

-   ときに、ユーザー モードのターゲットは、サービス アプリケーションです。 これらのターゲットをデバッグする方法の詳細については、次を参照してください。[サービス アプリケーションのデバッグ](debugging-a-service-application.md)します。

 

 





