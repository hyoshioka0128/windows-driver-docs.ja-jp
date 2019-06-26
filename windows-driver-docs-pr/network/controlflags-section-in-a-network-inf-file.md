---
title: ネットワーク INF ファイル内の ControlFlags セクション
description: ネットワーク INF ファイル内の ControlFlags セクション
ms.assetid: 384e56e3-8a64-4b47-ae9c-e9973733c7e7
keywords:
- INF ファイルの WDK ネットワーク、ControlFlags セクション
- ネットワーク INF ファイル、WDK ControlFlags セクション
- ControlFlags セクション WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65cdae07b06b1b4edfa8d2eacf85c25fa280024f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374944"
---
# <a name="controlflags-section-in-a-network-inf-file"></a>ネットワーク INF ファイル内の ControlFlags セクション





A **ControlFlags**ネットワーク INF ファイルのセクションは、ジェネリックに基づきます[ **INF ControlFlags セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)します。

**ControlFlags**ネットワーク INF ファイルのセクションは、1 つまたは複数に通常は**ExcludeFromSelect**エントリ。 各**ExcludeFromSelect**エントリを手動でインストール中にオプションとして、エンドユーザーに表示されないネットワーク コンポーネントを指定します。

**ControlFlags**ネットワーク INF ファイルのセクションを含める必要があります、 **ExcludeFromSelect**エントリ、インストールする各プラグ アンド プレイ アダプターを追加する必要のあるソフトウェアのコンポーネント手動ではなくプログラムによって、ユーザーがいます。

プラグ アンド プレイと互換性がないするアダプターがユーザーによって手動で追加する必要があります、ためには表示されません、 *ControlFlags*セクション。 たとえば、非 PnP ISA アダプター、および EISA アダプターする必要があります手動で追加するユーザー。 Windows XP およびそれ以降のオペレーティング システムはサポートされていないことおよび EISA アダプター非 PnP ISA アダプターに注意してください。

**注**  、 **ExcludeFromSelect** 、NCF よりも、エントリは、別の関数を実行します\_の HIDDEN 値、**特性**、エントリ *。DDInstall*セクション。 詳細については、次を参照してください。 [DDInstall セクション](ddinstall-section-in-a-network-inf-file.md)します。

 

**ExcludeFromSelect**エントリに一覧表示することから、アダプターまたはソフトウェア コンポーネントをできないように、**コンポーネントのインストールの選択** ダイアログ ボックス。 アダプターまたはコンポーネント、ただし、引き続きに表示される、**接続** ダイアログ ボックス。 NCF\_HIDDEN の値によってアダプターまたはコンポーネントが、ユーザー インターフェイスの任意の部分に表示されているを防ぎますなど、**接続** ダイアログ ボックス。

 

 





