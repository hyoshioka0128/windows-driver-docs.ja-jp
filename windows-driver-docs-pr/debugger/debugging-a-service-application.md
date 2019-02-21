---
title: サービス アプリケーションのデバッグ
description: サービス アプリケーションのデバッグ
ms.assetid: 1d1e24d5-8b6b-4ed5-84ad-b73356168b10
keywords:
- サービス アプリケーションのデバッグ
- 事後分析のデバッグ、サービス アプリケーションのデバッグ
- サービス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c40ac56795bcc2d316cbed96c3ea289eac23122
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537073"
---
# <a name="debugging-a-service-application"></a>サービス アプリケーションのデバッグ


A*サービス*とも呼ばれます、 *Windows サービス*は人間の介入なしで Windows 開始するように設計ユーザー モード プロセスです。 システムの起動時に、または Win32 API に含まれるサービスの機能を使用するアプリケーションによって自動的に開始されます。 サービスは、人間のユーザーのサービス コントロール パネルのユーティリティを使用しても起動できます。 すべてのサービスは、サービス コントロール マネージャー (SCM) のインターフェイスの規則に従う必要があります。

各サービスは 3 つの要素で構成されます。*サービス アプリケーション*、*サービス コントロール プログラム*、およびサービス コントロール マネージャー自体。 サービス アプリケーションがありますが (正しく) と呼ばれますしない「サービス」、実際にはサービスを構成する 3 つのコンポーネントのいずれか。 サービス アプリケーションは、ほとんどの種類のユーザー モード コードを含めることができます。 サービス コントロール プログラム コントロール サービス アプリケーションが起動して停止します。 サービス コントロール マネージャーは、Windows の一部です。

次のセクションでは、サービス アプリケーションをデバッグする方法について説明します。

[最適な方法の選択](choosing-the-best-method.md)

[サービス アプリケーションのデバッグの準備](preparing-to-debug-the-service-application.md)

[自動的にサービス アプリケーションのデバッグ](debugging-the-service-application-automatically.md)

[手動でサービス アプリケーションのデバッグ](debugging-the-service-application-manually.md)

サービス、サービス アプリケーション、サービス コントロール マネージャーの概要については、次を参照してください。 *Microsoft Windows internals 』。Microsoft Windows Server 2003、Windows XP、および Windows 2000* David A. Solomon して E. のある Mark Russinovich (4 th edition、Microsoft Press、2005)。

 

 





