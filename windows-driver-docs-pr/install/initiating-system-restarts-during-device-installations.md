---
title: デバイスのインストール中のシステムの再起動の開始
description: デバイスのインストール中のシステムの再起動の開始
ms.assetid: 52db2894-e759-4382-97de-5db7f268ff59
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a96876ac81b7b8fa15697588dfaebf4fc8debf1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325814"
---
# <a name="initiating-system-restarts-during-device-installations"></a>デバイスのインストール中のシステムの再起動の開始


システムの再起動、デバイスのインストールを完了するために必要なまれなケースでは、次の規則を使用します。

-   初期のインストール中にデバイスのインストーラーまたは共同インストーラーを要求できますシステムの再起動で DI_NEEDRESTART を設定して、 [ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346) と共に受信される構造体[デバイス インストールの関数コード](https://msdn.microsoft.com/library/windows/hardware/ff541307)します。 (これを行ってはいけませんしない限り、絶対に必要です)。

-   更新プログラムのインストール中にデバイスのインストール アプリケーションを呼び出すことができます[ **UpdateDriverForPlugAndPlayDevices**](https://msdn.microsoft.com/library/windows/hardware/ff553534)システムの再起動が必要かどうかを決定します。

 

 





