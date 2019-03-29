---
title: ユーザーモード デバッグ中のセキュリティ
description: ユーザーモード デバッグ中のセキュリティ
ms.assetid: e198c29a-d793-4974-8ee3-f26679bd70b4
keywords:
- セキュリティに関する考慮事項は、ユーザー モードのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f12e1df4c3f97408bc6c840177e3fc11597fbaee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573928"
---
# <a name="security-during-user-mode-debugging"></a>ユーザーモード デバッグ中のセキュリティ


## <span id="ddk_security_during_user_mode_debugging_dbg"></span><span id="DDK_SECURITY_DURING_USER_MODE_DEBUGGING_DBG"></span>


ユーザー モード デバッガーがアクティブで効果的に制御、コンピューター上のプロセスのできます。

セキュリティ上の問題がユーザー モードのデバッグ中に発生する可能性があります、3 つの可能な方法はあります。

-   破損または破壊の拡張 Dll を使用する場合、デバッガー以外、対象のアプリケーションを与えることがあります、予期しないアクションを実行する可能性があります。

-   可能性の破損または破壊のシンボル ファイルは、ターゲット以外のアプリケーションを与えることがあります、予期しないアクションを実行するようにデバッガーでもは可能性があります。

-   リモート デバッグ セッションを実行している場合、クライアントが予期しない可能性があります、サーバーにリンクしようとします。 または、クライアントが必要な可能性がありますしないと思われるアクションを実行しようとおそらくします。

予期しないリモート接続を防ぐ方法の推奨事項は、次を参照してください。[セキュリティ リモート デバッグ中に](security-during-remote-debugging.md)します。 ユーザー モードのデバッグ セッションをリモート クライアントの参加後、コンピューター上のプロセスへのアクセスを制限する方法はありません。

リモート デバッグを実行していない場合は、正しくないシンボル ファイルおよび拡張 Dll の注意する必要がありますもします。 シンボルまたは信頼する拡張機能は読み込まれません。

 

 





