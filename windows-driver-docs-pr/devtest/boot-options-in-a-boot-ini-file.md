---
title: Boot.ini ファイルでのブート オプション
description: Boot.ini は、システム パーティション、c:\Boot.ini 通常のルートにあるテキスト ファイルです。 Boot.ini ストア ブートは、これまでは、x86 および x64 ベース プロセッサを持つコンピューターの BIOS ファームウェアを使用してコンピューターをオプションします。
ms.assetid: a2593b6d-03df-49d1-ae77-efec4c2ac8be
keywords:
- Boot.ini files WDK
- ブート オプション WDK、Boot.ini ファイル
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e65b4cd98eec0588637899c148dc14e79db67ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557972"
---
# <a name="boot-options-in-a-bootini-file"></a>Boot.ini ファイルでのブート オプション

> [!IMPORTANT] 
> このトピックでは、Windows XP および Windows Server 2003 でサポートされるブート オプションについて説明します。 Windows 8、Windows Server 2012、Windows 7、Windows Server 2008、または Windows Vista のブート オプションを変更する場合は、[Windows Vista 以降のブート オプション](boot-options-in-windows-vista-and-later.md)を参照してください。\]

Boot.ini はシステム パーティション、通常は c: のルートにあるテキスト ファイル\\Boot.ini します。 Boot.ini ストア ブートは、これまでは、IA ベースおよび x64 ベース プロセッサを搭載したコンピューターの BIOS ファームウェアを使用してコンピューターをオプションします。 Windows Server 2003 および Windows NT ファミリのオペレーティング システムの以前のバージョンでは、コンピューターが起動するときに、Windows ブート ローダー、"ntldr"と呼ばれる、Boot.ini ファイルを読み取り、およびブート メニューに各オペレーティング システムのエントリが表示されます。 次に、ntldr が Boot.ini ファイル内の設定に従って、選択したオペレーティング システムを読み込みます。

NTFS ドライブで、既定、**システム**、**隠し**、**アーカイブされた**、および**読み取り専用**Boot.ini; を保護する属性が設定されてただし、Administrators グループのメンバーは、これらの属性を変更できます。 ファイル属性は、ブート ローダーの操作には影響しません。

次のセクションでは、の簡単な Boot.ini をについて説明して、ブート オプションは、高度なテクノロジのパーソナル コンピューターのコンピューターに固有の側面について説明します (PC に/)、BIOS ファームウェアを入力します。

このセクションの内容:

- [Boot.ini ファイルの概要](overview-of-the-boot-ini-file.md)
- [Boot.ini ファイルの編集](editing-the-boot-ini-file.md)
- [Boot.ini ファイルをバックアップします。](backing-up-the-boot-ini-file.md)

このドキュメントでは、Boot.ini のドライバー開発者およびテスト担当者に特別な関心のある側面について説明します。 Boot.ini パラメーターの完全な一覧を参照してください。 [Windows XP と Windows Server 2003 の Boot.ini ファイルの使用可能なスイッチ オプション](https://go.microsoft.com/fwlink/p/?linkid=137742)、Microsoft サポート web サイトに関するトピック。
