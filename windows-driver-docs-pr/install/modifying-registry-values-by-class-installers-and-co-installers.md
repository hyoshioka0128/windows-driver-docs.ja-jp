---
title: クラス インストーラーと共同インストーラーでのレジストリ値の変更
description: クラス インストーラーと共同インストーラーでのレジストリ値の変更
ms.assetid: 2D4B907A-622B-4b1b-A692-8E858F770F70
keywords:
- レジストリ WDK デバイスのインストール、レジストリ値を変更します。
- レジストリ WDK デバイスのインストール、レジストリの値を変更するクラスのインストーラー
- レジストリ WDK デバイスのインストール、レジストリ値、共同インストーラーを変更します。
- クラスのインストーラー WDK デバイスのインストール、レジストリ値を変更します。
- 共同インストーラー WDK デバイスのインストール、レジストリ値を変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1230f334bcc8a17c0f6510210c1e8b52fb0f193c
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65456374"
---
# <a name="modifying-registry-values-by-class-installers-and-co-installers"></a>クラス インストーラーと共同インストーラーでのレジストリ値の変更


**注**  ユニバーサルまたはモバイルのドライバー パッケージでは、このセクションで説明する機能はサポートされていません。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

特定の状況では、except*クラス インストーラー*と*co-installer*作成、変更、またはレジストリ値で使用するために予約されているを削除するには、標準レジストリ関数を呼び出してはならない、オペレーティング システム。

次に、この規則の例外を示します。

-   必要な場合は、クラスのインストーラーと共同インストーラー関数を使用できます標準レジストリのレジストリ値を変更、 **HKLM\\ソフトウェア**サブツリーです。

    **注**  クラスのインストーラーと共同インストーラーが、デバイスの内のエントリとしてカスタムのデバイスのプロパティを保存ことを強くお勧め*ソフトウェア キー*します。

     

-   クラスのインストーラーと共同インストーラーの値を変更できる、 [RunOnce レジストリ キー](runonce-registry-key.md)します。 ただし、この値で構成への呼び出しのみの*Rundll32.exe*します。

    クラスのインストーラーと共同インストーラーが使用する方法についての制限に従う必要があります、 [RunOnce レジストリ キー](runonce-registry-key.md)で[INF ファイル](overview-of-inf-files.md)します。 具体的には、このレジストリ キーは、ソフトウェアのデバイス列挙子 (SWENUM) を使用して列挙されるソフトウェア専用デバイスのインストールにのみ使用する必要があります。

-   クラスのインストーラーと共同インストーラーを変更できる、 **CoInstallers32**と**EnumPropPages32**デバイスのレジストリ値*ソフトウェア キー*インストーラーの処理[ **DIF_REGISTER_COINSTALLERS** ](https://msdn.microsoft.com/library/windows/hardware/ff543715)要求。

次のガイドラインは、クラスのインストーラーや共同インストーラーによってレジストリ値を安全に変更する後にする必要があります。

-   クラスのインストーラーと共同インストーラーを使用する必要がありますまず[ **SetupDiCreateDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550973)または[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)へのハンドルを開く変更するレジストリ キーです。 ハンドルが開かれた後は、レジストリ値を変更するのにクラスのインストーラーと共同インストーラーが標準レジストリ関数を使用できます。

-   クラスのインストーラーと共同インストーラーを使用する必要がありますいない**SetupDiDeleteDevRegKey**または*ハードウェア キー*デバイス。 詳細については、次を参照してください。[デバイスのレジストリ キーを削除する](deleting-the-registry-keys-of-a-device.md)します。

詳細については、標準レジストリ関数は、次を参照してください。[レジストリ関数](https://go.microsoft.com/fwlink/p/?linkid=194529)します。

 

 





