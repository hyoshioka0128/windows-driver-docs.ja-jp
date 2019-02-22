---
title: カーネル モードのダンプ ファイルを有効にします。
description: カーネル モードのダンプ ファイルを有効にします。
ms.assetid: 4faf389f-764e-4439-9e45-fdd53890b0d1
keywords:
- カーネル モードのダンプ ファイルを有効にすると、ダンプ ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10156aa9bda2a55778c0ded4b5ec53f30cbb5e92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560222"
---
# <a name="enabling-a-kernel-mode-dump-file"></a>カーネル モードのダンプ ファイルを有効にします。


## <span id="ddk_enabling_a_kernel_mode_dump_file_dbg"></span><span id="DDK_ENABLING_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


システムのクラッシュ時に、Windows のクラッシュ ダンプ設定は、ダンプ ファイルを作成するかどうかをそのため、ダンプ ファイルのサイズとなりますを決定します。

Windows コントロール パネル では、カーネル モードのクラッシュ ダンプの設定を制御します。 システム管理者だけでは、これらの設定を変更できます。

これらの設定を変更するには**コントロール パネルの &gt;システムとセキュリティ&gt;システム**します。 クリックして**システムの詳細設定**します。 [**起動と回復**、] をクリックして**設定**します。

次のダイアログ ボックスが表示されます。

![起動と回復 ダイアログ ボックスのスクリーン ショット](images/crashpanel.png)

**デバッグ情報の書き込み**、カーネル モードのダンプ ファイルの設定を指定することができます。 クラッシュが特定の 1 つだけのダンプ ファイルを作成できます。 参照してください[カーネル モードのダンプ ファイルの変形](varieties-of-kernel-mode-dump-files.md)異なるダンプ ファイルの設定の説明についてはします。

選択または選択解除することも、**システム ログにイベントを書き込む**と**自動的に再起動**オプション。

選択した設定は、システムのクラッシュが偶発的なかどうかや、これが、デバッガーによって発生したかどうかに関係なく、システムのクラッシュによって作成された任意のカーネル モード ダンプ ファイルに適用されます。 参照してください[強制的にシステムのクラッシュ](forcing-a-system-crash.md)については、意図的なクラッシュが発生します。

ただし、これらの設定がによって作成されたダンプ ファイルを影響しないで、 [ **.dump** ](-dump--create-dump-file-.md)コマンド。 参照してください[、ダンプ ファイルせず、システムがクラッシュする作成](creating-a-dump-file-without-a-system-crash.md)についてはこのコマンドを使用します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネル モードのダンプ ファイル](kernel-mode-dump-files.md)

[さまざまなカーネル モードのダンプ ファイル](varieties-of-kernel-mode-dump-files.md)

 

 






