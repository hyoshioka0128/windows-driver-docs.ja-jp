---
title: デバイスのインストール中のシステムの再起動の開始
description: デバイスのインストール中のシステムの再起動の開始
ms.assetid: 52db2894-e759-4382-97de-5db7f268ff59
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc02c2773262d29759bd644709a61814fa6bb2b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370012"
---
# <a name="initiating-system-restarts-during-device-installations"></a>デバイスのインストール中のシステムの再起動の開始


システムの再起動、デバイスのインストールを完了するために必要なまれなケースでは、次の規則を使用します。

-   初期のインストール中にデバイスのインストーラーまたは共同インストーラーを要求できますシステムの再起動で DI_NEEDRESTART を設定して、 [ **SP_DEVINSTALL_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a) と共に受信される構造体[デバイス インストールの関数コード](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))します。 (これを行ってはいけませんしない限り、絶対に必要です)。

-   更新プログラムのインストール中にデバイスのインストール アプリケーションを呼び出すことができます[ **UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)システムの再起動が必要かどうかを決定します。

 

 





