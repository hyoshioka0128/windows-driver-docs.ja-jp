---
title: アプリケーション エラーのデバッグ
description: アプリケーション エラーのデバッグ
ms.assetid: c4118acb-2566-441a-8481-dee4bfdb03ba
keywords:
- アプリケーションのエラー
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fcf7d0401c12c06b8556f8d0e2b2048cf3aaefe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377203"
---
# <a name="debugging-an-application-failure"></a>アプリケーション エラーのデバッグ


## <span id="ddk_debugging_an_application_failure_dbg"></span><span id="DDK_DEBUGGING_AN_APPLICATION_FAILURE_DBG"></span>


ユーザー モード アプリケーションでは、さまざまなエラーです。

エラーの最も一般的な種類は、アクセス違反、配置エラー、例外、クリティカル セクションのタイムアウト (デッドロック)、およびページ I/O エラー。

アクセス違反とデータ型のずれは、最も一般的なデータです。 無効なポインターが逆参照されるときに通常発生します。 変更履歴、エラーの原因となった関数と、以前の関数エラーが発生した関数に無効なパラメーターを渡すことがあると考えです。

ユーザー モード例外では、多くの考えられる原因があります。 不明な例外が発生する場合は、可能であれば ntstatus.h または winerror.h で探します。

クリティカル セクションのタイムアウト (またはデッドロックの可能性) は、長い間、クリティカル セクションの 1 つのスレッドが待機しているときに発生します。 これらは、デバッグやスタック トレースの詳細に分析が困難です。

ページで I/O エラーは、ほとんどの場合、ハードウェアの障害です。 確認する ntstatus.h にステータス コードを再確認することができます。

 

 





