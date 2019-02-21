---
title: レジストリ キーを安全にアクセスします。
description: レジストリ キーを安全にアクセスします。
ms.assetid: 81203790-66CB-42ee-82F8-2F0FFF04DF10
keywords:
- レジストリ WDK デバイスのインストール、レジストリ キーを安全にアクセスします。
- キーのレジストリへのアクセスに安全に WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62b7e171d77620bdd977ed66e48a66a9cf36f96d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556907"
---
# <a name="accessing-registry-keys-safely"></a>レジストリ キーを安全にアクセスします。


お客様の問題が頻繁に由来するサード パーティ製などの外部コンポーネント[デバイス インストール アプリケーション](writing-a-device-installation-application.md)以下を実行します。

-   重要なレジストリ キーを削除します。

-   重要なレジストリ キーのアクセス許可を変更します。

レジストリ キーの KEY_ALL_ACCESS のアクセス許可を使用して外部コンポーネントで発生する問題の多くが原因です。 以降では、Windows Server 2003、 [ **SetupDiCreateDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550973) KEY_READ と KEY_WRITE のみがアクセス許可と KEY_ALL_ACCESS されませんをアクセスを許可します。 Windows Vista 以降では、追加の KEY_ALL_ACCESS 制限が適用されます。

レジストリ キーを安全にアクセスする次のガイドラインに従います。

-   サーバーやワークステーションを使用し、*ソフトウェア キー*デバイス。

    これらの関数は、アクセス許可の制限に起因する一般的な問題に対処します。

-   レジストリ キーの形式と場所は、Windows の異なるバージョン間で変更可能性があります。 場所、形式、またはレジストリ キーまたはデバイスとドライバーのインストールに使用される値の意味について想定しないでください。

    レジストリ キーおよびツリーに関する詳細については、次を参照してください。[レジストリ ツリーとデバイスとドライバーのキー](registry-trees-and-keys.md)します。

-   直接アクセスするか、デバイスの内部設定を変更するのには、レジストリを使用しません。

-   各タスクは、次のように必要な最小限のアクセス許可のみを要求します。

    -   KEY_SET_VALUE

    -   KEY_CREATE_SUB_KEY

    -   KEY_QUERY_VALUE

    -   KEY_ENUMERATE_SUB_KEYS

-   直接デバイス セットアップ クラスのキーで開かないでレジストリ。 レジストリ キーと同様にデバイス セットアップ クラスのキーの名前と場所は、Windows のバージョン間で変更可能性があります。

    デバイス セットアップ クラスのキーを安全に開くには、次のガイドラインに従います。

    -   使用[ **SetupDiOpenClassRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552065)します。

    -   使用[ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)で DIOCR_INSTALLER を設定して、*フラグ*パラメーター。

-   直接インターフェイス クラスのデバイスのキーで開かないでレジストリ。 レジストリ キーと同様に Windows のバージョン間でデバイス インターフェイス クラスのキーの名前と場所を変更可能性があります。

    インターフェイス クラスのデバイスのキーを安全に開くを使用して[ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)で DIOCR_INSTALLER を設定して、*フラグ*パラメーター。

-   INF ディレクティブのみを使用すると、オペレーティング システムで使用するために予約されているレジストリ キーを変更できます。 詳細については、次を参照してください。 [INF ディレクティブの概要](summary-of-inf-directives.md)します。

-   *インストーラー クラス*と*co-installer*作成、変更、またはオペレーティング システムで使用するために予約されているレジストリ値を削除するレジストリ関数を呼び出すことはできません。

    詳細については、次を参照してください。[クラスのインストーラーと共同インストーラーによってレジストリにアクセスする](accessing-the-registry-by-class-installers-and-co-installers.md)します。

レジストリ キーのアクセス許可の詳細については、次を参照してください。[レジストリ キーのセキュリティとアクセス権](https://go.microsoft.com/fwlink/p/?linkid=194542)します。

 

 





