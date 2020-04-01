---
title: ブート オプションの編集
description: ブート オプションの編集
ms.assetid: b50b3ac8-154a-4c26-907f-11e274a5c7c8
keywords:
- ブートオプション WDK、編集
- ブートオプションの編集
- Bootcfg ツール
- カスタムブートオプション WDK
- ブートエントリ WDK
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9d06f21d2b022a2ee8028e94d09b976388a8d542
ms.sourcegitcommit: a2d1c389f0f413cc967068cbde22a5598e5a5d57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2020
ms.locfileid: "80516775"
---
# <a name="editing-boot-options"></a>ブート オプションの編集

このセクションでは、Windows Server 2008、Windows Server 2012、または Windows 7 以降を実行しているコンピューターでブートオプションを編集するための実用的なガイドを示します。 ブートオプションの基本要素をカスタマイズするための詳細な手順について説明します。

このセクションでは、オペレーティングシステムに付属のツールである BCDEdit を使用する方法について説明します。 BCDEdit コマンドの構文の詳細については、「 **bcdedit/?」と**入力してください。 または**bcdedit/?** コマンドプロンプトウィンドウのトピック。 詳細については、「 [BCDEdit Options Reference](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference) 」を参照してください。

> [!NOTE]
> BCDEdit のオプションを設定する前に、コンピューターで BitLocker とセキュア ブートを無効にするか中断することが必要になる場合があります。

ブートエントリパラメーターを編集して Windows の機能を有効または無効にする方法については、「[ブートパラメーターの使用](using-boot-parameters.md)」を参照してください。

ブートオプションでオペレーティングシステムの機能を構成するには

- 同じオペレーティングシステムから既存のブートエントリをコピーすることによって、オペレーティングシステムの[新しいブートエントリを追加](adding-boot-entries.md)します。

- 新しく作成されたブートエントリの[フレンドリ名を変更](changing-the-friendly-name-of-a-boot-entry.md)して、ブートメニューで識別できるようにします。

- Windows の機能を有効にして構成する[ブートエントリにパラメーターを追加](changing-boot-parameters.md)します。

次に、テストをより迅速かつ簡単に行うことができます。

- [新しいブートエントリを既定のエントリに](changing-the-default-boot-entry.md)します。

-  [ブートメニューのタイムアウトを変更](changing-the-boot-menu-time-out.md)します。Windows がすぐに起動するように、ブートメニューのタイムアウトを短縮することができます。 または、ブートメニューのタイムアウトを長くして、優先ブートエントリを選択するための十分な時間を確保します。

## <a name="related-topics"></a>関連トピック 
 [BCDEdit のコマンドラインオプション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/bcdedit-command-line-options)

> [!CAUTION]
> BCD を変更するために BCDEdit を使用するには、管理者特権が必要です。 **BCDEdit /set** コマンドを使用して一部のブート エントリ オプションを変更すると、コンピューターが動作しなくなる可能性があります。 別の方法として、システム構成ユーティリティ (MSConfig.exe) を使用してブート設定を変更します。
