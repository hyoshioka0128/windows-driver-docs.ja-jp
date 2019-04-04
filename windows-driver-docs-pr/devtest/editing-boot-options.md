---
title: ブート オプションの編集
description: ブート オプションの編集
ms.assetid: b50b3ac8-154a-4c26-907f-11e274a5c7c8
keywords:
- ブート オプション、WDK の編集
- ブート オプションの編集
- Bootcfg ツール
- カスタムのブート オプション WDK
- WDK のブート エントリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77f0cb3bd7bb87c22721bbbe76f598697e3c9e9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535576"
---
# <a name="editing-boot-options"></a>ブート オプションの編集


## <span id="ddk_editing_boot_options_tools"></span><span id="DDK_EDITING_BOOT_OPTIONS_TOOLS"></span>


このセクションでは、Windows 10、Windows 8、Windows Server 2012、Windows 7、または Windows Server 2008 を実行するコンピューターでブート オプションを編集するための実用ガイドです。 ブート オプションの基本要素をカスタマイズするためのステップ バイ ステップの手順が推奨されています。

このセクションでは、BCDEdit、オペレーティング システムに含まれているツールを使用する方法について説明します。 BCDEdit のコマンド構文の詳細については、入力**bcdedit/でしょうか。** または**bcdedit/でしょうか。トピック**コマンド プロンプト ウィンドウでします。 参照してください[BCD のブート オプションの参照](https://msdn.microsoft.com/library/windows/hardware/ff542205)詳細についてはします。

**注**  BCDEdit のオプションを無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要がありますを設定する前にします。

 

Windows の機能を無効にするブート エントリ パラメーターを編集する方法については、[ブート パラメーターを使用して](using-boot-parameters.md)を参照してください。

ブート オプションでは、オペレーティング システムの機能を構成します。

-   [新しいブート エントリを追加](adding-boot-entries.md)同じオペレーティング システムから既存のブート エントリをコピーして、オペレーティング システム。

-   [フレンドリ名を変更](changing-the-friendly-name-of-a-boot-entry.md)の新しく作成されたブート エントリのブート メニューで識別できるようにします。

-   [ブート エントリにパラメーターを追加](changing-boot-parameters.md)を有効にし、Windows の機能を構成します。

後も迅速かつ容易にテストを作成します。

-   [新しいブート エントリの既定のエントリを作成する](changing-the-default-boot-entry.md)します。

-   [ブート メニュー タイムアウト値を変更](changing-the-boot-menu-time-out.md)します。その Windows が迅速に起動するように、ブート メニュー タイムアウトを短縮できます。 または、優先のブート エントリを選択できる十分な時間があるように、ブート メニュー タイムアウトを長きます。

 

 





