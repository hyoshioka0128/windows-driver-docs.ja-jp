---
title: システム イベントの監査ログの有効化
description: システム イベントの監査ログの有効化
ms.assetid: a4206f06-0c81-407e-80aa-4f6b08cb2a70
keywords:
- WDK のドライバー署名の詳細なログ記録
- セキュリティ監査ポリシー WDK ドライバー署名
- システム監査ポリシー WDK ドライバー署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17628840a7d2bc6d7bda4d9399fa82b1c02fb4fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357763"
---
# <a name="enabling-the-system-event-audit-log"></a>システム イベントの監査ログの有効化


このトピックは、次の情報で構成されます。

[セキュリティ監査ポリシーを有効にする方法](#how-to-enable-security-audit-policy)

[コードの整合性の診断イベントの詳細なログ記録を有効にする方法](#how-to-enable-verbose-logging-of-code-integrity-diagnostic-events)

### <a href="" id="how-to-enable-security-audit-policy"></a> セキュリティ監査ポリシーを有効にする方法

監査ログの読み込みエラーをキャプチャする、セキュリティ監査ポリシーを有効にするには、次の手順に従います。

1.  管理者特権のコマンド プロンプト ウィンドウを開きます。 管理者特権のコマンド プロンプト ウィンドウを開くには、デスクトップ ショートカットを作成*Cmd.exe*を右クリックし、 *Cmd.exe*ショートカット、および選択**管理者として実行**します。

2.  管理者特権のコマンド プロンプト ウィンドウで、次のコマンドを実行します。

    ```cpp
    Auditpol /set /Category:System /failure:enable
    ```

3.  変更を反映するには、コンピューターを再起動します。

Auditpol を使用して、セキュリティ監査を有効にする方法を次のスクリーン ショットを示します。

![セキュリティ監査を有効にする auditpol の使用方法を示すコマンド プロンプト ウィンドウのスクリーン ショット](images/driver-signing-enable-auditpol.png)

### <a href="" id="how-to-enable-verbose-logging-of-code-integrity-diagnostic-events"></a> コードの整合性の診断イベントの詳細なログ記録を有効にする方法

詳細ログ記録を有効にするのには、次の手順を実行します。

1.  管理者特権のコマンド プロンプト ウィンドウを開きます。

2.  実行*Eventvwr.exe*コマンド行にします。

3.  下、**イベント ビューアー**イベント ビューアーの左側のウィンドウでフォルダーは、次の一連のサブフォルダーを展開します。

    1.  **アプリケーションとサービス ログ**

    2.  **Microsoft**

    3.  **Windows**

4.  展開、**コードの整合性**の下のサブフォルダー、 **Windows**フォルダーのコンテキスト メニューを表示します。

5.  選択**ビュー**します。

6.  選択**分析およびデバッグ ログ**します。 イベント ビューアーが含まれるサブツリーを表示し、 **Operational**フォルダーと**Verbose**フォルダー。

7.  右クリック**Verbose**選び**プロパティ**ポップアップのコンテキスト メニューから。

8.  選択、**全般** タブで、**プロパティ**クリックしてダイアログ ボックスで、**ログ記録を有効にする**プロパティ ページの中央付近オプション。 これは、詳細ログ記録を有効になります。

9.  変更を反映するには、コンピューターを再起動します。

 

 





