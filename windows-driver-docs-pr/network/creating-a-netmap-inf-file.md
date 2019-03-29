---
title: Netmap.inf ファイルの作成
description: Netmap.inf ファイルの作成
ms.assetid: 0f9b4f57-717c-4f11-b0c6-d117a949ab38
keywords:
- ネットワーク コンポーネントのアップグレード WDK、netmap.inf ファイルのファイル
- ネットワーク コンポーネント、WDK netmap.inf ファイルのファイルをアップグレードします。
- WDK netmap.inf ファイルのファイル
- ベンダーから提供されたファイルの WDK netmap.inf ファイルのファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d05da941108e5db69604c8aeabfaaea786d750e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579462"
---
# <a name="creating-a-netmapinf-file"></a>Netmap.inf ファイルの作成





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

Netmap.inf ファイル ファイル内のエントリで指定されたディレクトリのいずれかに存在するベンダーから提供されたファイルでは、 **OemNetUpgradeDirs**のセクションを[netupg.inf](creating-a-netupg-inf-file.md)ファイルまたはディレクトリを含む944 netupgrd.dll します。 Netmap.inf ファイル ファイル:

-   ネットワーク コンポーネントのアップグレード前のデバイス ID をコンポーネントの Microsoft Windows 2000 またはそれ以降のデバイス ID をマップします。

-   ネットワーク移行 NetSetup が読み込まれる DLL を指定します

-   必要に応じて別のヘルプ メッセージ ファイルを指定します

これらのコンポーネントが Windows 2000 およびそれ以降の動作のインストール時に自動的にアップグレードするために、Windows 2000 またはそれ以降のオペレーティング システムのアップグレードのサポートを組み込みのネットワーク コンポーネントで netmap.inf ファイルのベンダーから提供されたファイルが必要ないです。システム。

ここでは、次のトピックについて説明します。

-   [Netmap.inf ファイル ファイル内の Id のマッピング](mapping-ids-in-a-netmap-inf-file.md)
-   [Netmap.inf ファイル ファイルで、アップグレードの DLL の指定](specifying-the-upgrade-dll-in-a-netmap-inf-file.md)
-   [Netmap.inf ファイル ファイルに代替のヘルプ メッセージ ファイルを指定します。](specifying-alternative-help-message-files-in-a-netmap-inf-file.md)

 

 





