---
title: SetupAPI
description: SetupAPI
ms.assetid: aa12ec50-2842-4ddd-9fc5-84436d69ea7a
keywords:
- SetupAPI WDK デバイス インストールでは、関数
- SetupAPI 関数の詳細については、SetupAPI 関数 WDK、
- WDK の SetupAPI 関数
- デバイス セットアップ WDK デバイスのインストール、SetupAPI
- デバイスのインストール、WDK SetupAPI
- デバイス、WDK SetupAPI をインストールします。
- WDK SetupAPI 関数
- デバイスのインストール、WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c8557f28c42be16c703f4b4e256e5c4b50c6c21
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348646"
---
# <a name="setupapi"></a>SetupAPI


セットアップ アプリケーション プログラミング インターフェイス (SetupAPI) では、2 つの関数のセットを提供するシステム コンポーネントです。

-   [一般的なセットアップ関数](using-general-setup-functions.md)

-   [デバイス インストールの機能](using-device-installation-functions.md)

デバイスのインストール ソフトウェアは、これらの関数を使用してでのカスタム操作を実行する[*クラス インストーラー*](writing-class-installers-and-co-installers.md)、 [*共同インストーラー*](writing-a-co-installer.md)、[*デバイス インストール アプリケーション*](writing-a-device-installation-application.md)します。

Driver Install Frameworks (DIFx) をデバイス インストールのアプリケーションには、プラグ アンド プレイ (PnP) 関数のドライバーをインストールし、アプリケーション ソフトウェアの間の関連付けを管理する低水準の SetupAPI 操作を抽象化する高度なツールを提供します、ドライバーです。 DIFx ツールでは、PnP ドライバーとデバイスのアプリケーション ソフトウェアをインストールするインストール アプリケーションを必要とする機能を提供する場合、インストール アプリケーションは、SetupAPI 関数を直接呼び出す代わりに DIFx ツールを使用する必要があります。 ただし、共同インストーラーおよびクラスのインストーラーは、デバイスまたはすべてのデバイスでのカスタム操作を実行することによって、既定のインストール操作を支援する Microsoft Win32 Dll を[デバイス セットアップ クラス](device-setup-classes.md)します。 通常、これらの操作には、Win32 関数と SetupAPI 関数への直接呼び出しが必要です。

このセクションには、使用する方法について一般的な情報を提供する、次のトピックが含まれています、[一般的なセットアップ関数](using-general-setup-functions.md)と[デバイス インストールの機能](using-device-installation-functions.md)SetupAPI が用意されています。

[一般的なセットアップ関数を使用します。](using-general-setup-functions.md)

[デバイス インストールの機能を使用します。](using-device-installation-functions.md)

[SetupAPI の一般的な使用方法](typical-setupapi-usage.md)

[SetupAPI の使用に関するガイドライン](guidelines-for-using-setupapi.md)

**注**  SetupAPI でセットアップの機能のサブセットのみを説明します。 この API の詳細については、次を参照してください。[セットアップ API](https://docs.microsoft.com/windows/desktop/SetupApi/setup-api-portal)します。

 

 

 





