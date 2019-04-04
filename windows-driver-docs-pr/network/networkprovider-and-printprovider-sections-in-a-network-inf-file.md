---
title: ネットワーク INF ファイル内の NetworkProvider および PrintProvider セクション
description: ネットワーク INF ファイル内の NetworkProvider および PrintProvider セクション
ms.assetid: 9ce32644-2b11-4c03-9743-d678ff8de229
keywords:
- INF ファイルの WDK ネットワーク、した PrintProvider セクション
- ネットワーク INF ファイル、WDK した PrintProvider セクション
- INF ファイルの WDK ネットワーク、NetworkProvider セクション
- ネットワーク INF ファイル、WDK NetworkProvider セクション
- した PrintProvider セクション WDK ネットワーク
- NetworkProvider セクション WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23e57b7f747f1ca25cd5c0c8738febc77dbc5b0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571621"
---
# <a name="networkprovider-and-printprovider-sections-in-a-network-inf-file"></a>ネットワーク INF ファイル内の NetworkProvider および PrintProvider セクション





**NetClient**コンポーネントはネットワーク サービスをユーザー アプリケーションに提供するため、ネットワーク プロバイダーにすると見なされます。 ネットワークおよび NetWare クライアント用の Microsoft クライアントの例に示します**NetClient**コンポーネント。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

ネットワーク プロバイダーだけでなく、 **NetClient**コンポーネントは、印刷プロバイダーをすることもできます。 印刷プロバイダーは、ネットワーク経由でユーザーのアプリケーションへの印刷サービスを提供します。

A **NetClient**コンポーネントは、ネットワーク プロバイダーとして必ずインストールされます。 インストールする INF ファイル、 **NetClient**次の少なくとも 1 つが true でない限り、コンポーネントがコンポーネントの NetworkProvider セクションを必要ありません。

-   別のデバイス名はコンポーネントを指定します。

-   使用するため、コンポーネントの短い名前が指定されて、 **「net view**コマンド。 詳細については、[、NetworkProvider セクションを含む](including-a-networkprovider-section.md)を参照してください。

インストールする、INF、 **NetClient**印刷プロバイダーであるコンポーネントを含める必要があります、**した PrintProvider**そのコンポーネントのセクション。 詳細については、[、した PrintProvider セクションを含む](including-a-printprovider-section.md)を参照してください。

インストールする INF ファイル、 **NetClient**コンポーネントも含める必要があります、*追加レジストリ セクション*(によって参照される、 **AddReg**ディレクティブで、 *サービスのインストール-セクション*コンポーネント) を追加する、 **NetworkProvider**をコンポーネントのキー**サービス**キー。 詳細については、[NetClient コンポーネントのプロバイダーのパスと名前を指定する](specifying-the-name-and-provider-path-for-a-netclient-component.md)を参照してください。

 

 





