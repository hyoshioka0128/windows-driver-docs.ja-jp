---
title: ネットワーク アップグレード プロセス
description: ネットワーク アップグレード プロセス
ms.assetid: f89cb7c2-8375-4326-94c8-70e2a5e3a1f7
keywords:
- ネットワーク コンポーネントをアップグレード WDK、フェーズ
- WDK のネットワーク コンポーネントのアップグレード フェーズします。
- 応答ファイルの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b95f7e0208037bed8f67e32057eae9160864fa3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350818"
---
# <a name="the-network-upgrade-process"></a>ネットワーク アップグレード プロセス





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

ネットワークのアップグレード プロセスは、次のように簡単にまとめることができますが、3 つのフェーズに分かれています。

-   **Winnt32 フェーズ**

    Winnt32.exe は NetSetup を呼び出します。 NetSetup では、ネットワーク コンポーネントに固有の情報を応答ファイルに書き込み、任意のベンダーから提供されたネットワークの移行の Dll を呼び出します。 Dll は、コンポーネント固有の情報を応答ファイルを書き込みます。 Winnt32.exe は、システムのアップグレード中に、Microsoft Windows 2000 またはそれ以降のファイルをコピーし、システム上のブート セクターを準備します。 テキスト モードに、システムでブートされます。

-   **テキスト モードのフェーズ**

    インストール メッセージは、青、テキスト ベースの画面に表示されます。 セットアップでは、基本的な Windows 2000 またはそれ以降のインストールを実行します。 システムは、フル インストール モードにし、起動します。

-   **GUI モードのフェーズ**

    NetSetup 処理、winnt.sif ファイルとも呼ばれる、応答ファイルには、ネットワーク コンポーネントをインストールします。 Dll のネットワーク移行をユーザー インターフェイスを表示できるユーザーまたはシステム管理者は、ネットワーク コンポーネントのパラメーターの値を指定できます。 NetSetup またはネットワークの移行を DLL のいずれか、ネットワーク コンポーネントのアップグレード前のパラメーターの値を書き込みますが Windows 2000 またはそれ以降のレジストリ。

ネットワークのアップグレード プロセスのフェーズは、次のトピックで詳しく説明します。

[ネットワークのアップグレード プロセスの Winnt32 フェーズ](winnt32-phase-of-the-network-upgrade-process.md)

[ネットワークのアップグレード プロセスのテキスト モードのフェーズ](text-mode-phase-of-the-network-upgrade-process.md)

[ネットワークのアップグレード プロセスのフェーズをフル インストール モード](gui-mode-phase-of-the-network-upgrade-process.md)

 

 





