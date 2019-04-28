---
title: Netmap.inf ファイル内の代替ヘルプ メッセージ ファイルの指定
description: Netmap.inf ファイル内の代替ヘルプ メッセージ ファイルの指定
ms.assetid: 66ab7124-803a-4497-b5e0-98b47006dfb6
keywords:
- ネットワーク コンポーネントのアップグレード WDK、netmap.inf ファイルのファイル
- ネットワーク コンポーネント、WDK netmap.inf ファイルのファイルをアップグレードします。
- WDK netmap.inf ファイルのファイル
- デバイス Id の WDK netmap.inf ファイル
- ヘルプ メッセージ ファイルの WDK netmap.inf ファイル
- 別のヘルプ メッセージ ファイルの WDK netmap.inf ファイル
- ベンダーから提供されたファイルの WDK netmap.inf ファイルのファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90811d5ba23b3e3771e9c98461bb720fee3781a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378970"
---
# <a name="specifying-alternative-help-message-files-in-a-netmapinf-file"></a>Netmap.inf ファイル内の代替ヘルプ メッセージ ファイルの指定





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

Netmap.inf ファイルのファイルのいずれかのネットワーク コンポーネントのデバイス ID のマッピングを検出する NetSetup に失敗した場合は、互換性レポート ページ、ウィザードでは、このコンポーネントが一覧表示します。 このような各コンポーネントに関連付けられているとは、ヘルプ メッセージ ファイルです。

既定では、NetSetup に含まれているヘルプ メッセージが表示されます、 \\winntupg\\unsupmsg.txt ファイルで、システムで、HTML ブラウザーがインストールされている場合、 \\winntupg\\unsupmsg.htm ファイル。 必要に応じて、unsupmsg.txt をオーバーライドするカスタム メッセージ ファイルと unsupmsg.txt メッセージ ファイルを指定します。 たとえば、仕入先は、そのネットワーク コンポーネントの一部のみのアップグレードがサポートを提供する場合、ベンダーは特定のコンポーネントのアップグレードのサポートが指定されていないことを示すカスタム ヘルプ メッセージ ファイルを指定できます。

省略可能な**OemUpgradeHelpFiles** netmap.inf ファイルのファイルのセクションが 1 つ以上のカスタム ヘルプ メッセージ ファイルを指定します。 このセクションでは、各エントリには、次の形式があります。

*postupgrade-ID* = *text-name*, *htm-file*

それぞれの文字の説明は次のとおりです。

*postupgrade ID*が Windows 2000 またはネットワーク コンポーネントの以降のデバイス ID

*テキスト name*はパスとテキスト バージョンのカスタム ヘルプ メッセージ ファイルの名前

*htm ファイル*はパスと HTML バージョンのカスタム ヘルプ メッセージ ファイルの名前。

完全なパス名が指定されていない場合*テキスト name*または*htm ファイル*、たとえば、指定されたパスが、i386 ディレクトリに追加されます: \\i386\\mydirectory\\myfile.txt します。

Netmap.inf ファイルのファイルの次の例が含まれています、 **OemUpgradeHelpFiles**セクション。

```INF
[Version]
signature="$WindowsNT$

[OemNetProtocols]
Protocol1=Protoco1_2000
Protocol2=Protocol2_2000

[OemUpgradeSupport]
Protocol1=NotSupported
Protocol2=abc_upgrade.dll, abc.inf

[OemUpgradeHelpFiles]
Protoco11=helpmsg.txt, helpmsg.htm
```

Protocol1 のデバイス ID のマッピングを提供 netmap.inf ファイル ファイルのサンプルでは、Protocol1 のアップグレードのサポートは提供されません、場合でも、 **OemNetProtocols**セクション。 このマッピングは、Protocol1 の Windows 2000 のデバイス ID を指定します。 Windows 2000 のデバイス ID は、メッセージのヘルプ ファイルをネットワーク コンポーネントに関連付ける必要があります。

注意キーワード**NotSupported** Protocol1 に割り当てられている、 **OemUpgradeHelpFiles**セクション。 このキーワードは、移行 Protocol1 をアップグレードする DLL を読み込む必要がないことを示します。

**OemUpgradeHelpFiles**前の例では、Protoco11=helpmsg.txt helpmsg.htm エントリのセクションが Protocol1 の 2 つのカスタム ヘルプ メッセージ ファイルを指定します。 カスタム ヘルプ メッセージがこれらのファイルに含まれていることを示します、たとえば、仕入先が Protocol1 のアップグレードをサポートしていないことをユーザー必要がありますとは別にアップグレードして Protocol1 Protocol2 Windows 2000 またはそれ以降のシステムをアップグレードする前に。

 

 





