---
title: 信頼されたルート証明機関の証明書ストア
description: 信頼されたルート証明機関の証明書ストア
ms.assetid: c1969171-3691-4110-9530-693853728327
keywords:
- 証明書ストアの WDK
- ドライバー WDK、デジタル署名の署名
- 信頼されたルート証明機関証明書ストア WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87c95dc9919eeae52a0ea904386afffeb6f3517e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339514"
---
# <a name="trusted-root-certification-authorities-certificate-store"></a>信頼されたルート証明機関の証明書ストア


Windows Vista 以降、プラグ アンド プレイ (PnP) マネージャーは、デバイスとドライバーのインストール中にドライバー署名の検証を実行します。 ただし、次のステートメントが true の場合にのみ、PnP マネージャーは、デジタル署名を確認が正常にできます。

-   署名の作成に使用された署名証明書は、証明機関 (CA) によって発行されました。

-   CA の対応するルート証明書がインストールされている、*信頼されたルート証明機関証明書ストア*します。 そのため、信頼されたルート証明機関の証明書ストアには、Windows が信頼しているすべての Ca のルート証明書が含まれています。

既定では、信頼されたルート証明機関の証明書ストアは、一連は、Microsoft ルート証明書プログラムの要件を満たす公共の Ca で構成されます。 管理者は、信頼された Ca の既定のセットを構成し、ソフトウェアを検証するための独自のプライベート CA をインストールします。

**注**  プライベート CA ではないネットワーク環境の外部で信頼されているでしょう。

 

有効なデジタル署名することによって信頼性との整合性を[ドライバー パッケージ](driver-packages.md)します。 ただし、必ずしも、エンドユーザーまたはシステム管理者を暗黙で信頼ソフトウェア発行元。 ユーザーまたは管理者は、インストールまたはソフトウェア発行者およびアプリケーションの知識に基づいて、ケースの単位でアプリケーションを実行するかどうかを決定する必要があります。 既定では、発行元は、信頼済みでその証明書がインストールされている場合にのみ、[信頼された発行元証明書ストア](trusted-publishers-certificate-store.md)します。

信頼されたルート証明機関の証明書ストアの名前は*ルート。* 使用して、プライベート CA のルート証明書をコンピューターの信頼されたルート証明機関証明書ストアに手動でインストールすることができます、 [ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)ツール。

**注**  ドライバーの PnP マネージャーによって使用される検証ポリシーの署名は、プライベート CA のルート証明書がローカル コンピューターのバージョンのルート証明機関で以前にインストールされている必要があります証明書ストア。 詳細については、次を参照してください。[ローカル マシンと現在のユーザー証明書ストア](local-machine-and-current-user-certificate-stores.md)します。

 

証明書ストアの詳細については、次を参照してください。[ドライバー署名の変更では、Windows 10 バージョン 1607](https://blogs.msdn.microsoft.com/windows_hardware_certification/2016/07/26/driver-signing-changes-in-windows-10-version-1607/)と[ドライバー署名ポリシー](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-policy--windows-vista-and-later-)します。

 

 





