---
title: ネットワークの INF ファイルで ControlFlags セクション
description: ネットワークの INF ファイルで ControlFlags セクション
ms.assetid: 384e56e3-8a64-4b47-ae9c-e9973733c7e7
keywords:
- INF ファイルの WDK ネットワーク、ControlFlags セクション
- ネットワーク INF ファイル、WDK ControlFlags セクション
- ControlFlags セクション WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e64a7cdec2c73ebac5b9cd2ce539f31e091ebc5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553702"
---
# <a name="controlflags-section-in-a-network-inf-file"></a>ネットワークの INF ファイルで ControlFlags セクション





A **ControlFlags**ネットワーク INF ファイルのセクションは、ジェネリックに基づきます[ **INF ControlFlags セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546342)します。

**ControlFlags**ネットワーク INF ファイルのセクションは、1 つまたは複数に通常は**ExcludeFromSelect**エントリ。 各**ExcludeFromSelect**エントリを手動でインストール中にオプションとして、エンドユーザーに表示されないネットワーク コンポーネントを指定します。

**ControlFlags**ネットワーク INF ファイルのセクションを含める必要があります、 **ExcludeFromSelect**エントリ、インストールする各プラグ アンド プレイ アダプターを追加する必要のあるソフトウェアのコンポーネント手動ではなくプログラムによって、ユーザーがいます。

プラグ アンド プレイと互換性がないするアダプターがユーザーによって手動で追加する必要があります、ためには表示されません、 *ControlFlags*セクション。 たとえば、非 PnP ISA アダプター、および EISA アダプターする必要があります手動で追加するユーザー。 Windows XP およびそれ以降のオペレーティング システムはサポートされていないことおよび EISA アダプター非 PnP ISA アダプターに注意してください。

**注**  、 **ExcludeFromSelect** 、NCF よりも、エントリは、別の関数を実行します\_の HIDDEN 値、**特性**、エントリ *。DDInstall*セクション。 詳細については、次を参照してください。 [DDInstall セクション](ddinstall-section-in-a-network-inf-file.md)します。

 

**ExcludeFromSelect**エントリに一覧表示することから、アダプターまたはソフトウェア コンポーネントをできないように、**コンポーネントのインストールの選択** ダイアログ ボックス。 アダプターまたはコンポーネント、ただし、引き続きに表示される、**接続** ダイアログ ボックス。 NCF\_HIDDEN の値によってアダプターまたはコンポーネントが、ユーザー インターフェイスの任意の部分に表示されているを防ぎますなど、**接続** ダイアログ ボックス。

 

 





