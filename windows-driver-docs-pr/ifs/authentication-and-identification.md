---
title: 認証と ID
description: 認証と ID
ms.assetid: fe118cf3-05ce-43b1-b878-4bb99b97dc2e
keywords:
- 脅威を最小限に抑え、セキュリティ WDK ファイル システム
- WDK ファイル システムの認証
- WDK ファイル システムの識別
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89c7226c90c48c91c8a80a9c28dd2bfb01115f3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393032"
---
# <a name="authentication-and-identification"></a>認証と ID


## <span id="ddk_authentication_and_identification_if"></span><span id="DDK_AUTHENTICATION_AND_IDENTIFICATION_IF"></span>


認証または id の問題、個々 のサービスにこのタスクのままでは、ほとんどのドライバーは関与しません。 アクセスの管理は 1 つのケースを認証または id の処理でドライバーを関係になる可能性があります。 この場合、認証手順は、通常、セキュリティ参照モニターへの呼び出しを処理します。 認証と id の情報は、セキュリティ トークンを指定したスレッドまたはプロセスのセキュリティ資格情報をカプセル化する内部データ構造で通常、オペレーティング システムによって追跡されます。

 

 




