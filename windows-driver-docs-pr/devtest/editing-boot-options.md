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
ms.openlocfilehash: 5c305b2c8acf6ba04acaeb997da8da1a7d5d2289
ms.sourcegitcommit: 2c8c13ed8d8f11eccf4c4ffb492c64099003b6a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74681889"
---
# <a name="editing-boot-options"></a>ブート オプションの編集

このセクションでは、Windows Server 2008、Windows Server 2012、または Windows 7 以降を実行しているコンピューターでブートオプションを編集するための実用的なガイドを示します。 ブートオプションの基本要素をカスタマイズするための詳細な手順について説明します。

このセクションでは、オペレーティングシステムに付属のツールである BCDEdit を使用する方法について説明します。 BCDEdit コマンドの構文の詳細については、「 **bcdedit/?」と**入力してください。 または**bcdedit/?** コマンドプロンプトウィンドウのトピック。 詳細については、「 [BCD ブートオプションリファレンス](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference)」を参照してください。

> [!NOTE]
> BCDEdit オプションを設定する前に、コンピューターで BitLocker とセキュアブートを無効にしたり、中断したりすることが必要になる場合があります。

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
> BCDEdit を使用して BCD を変更するには、管理者特権が必要です。 **BCDEdit/set**コマンドを使用して一部のブートエントリオプションを変更すると、コンピューターが動作しなくなる可能性があります。 別の方法として、システム構成ユーティリティ (Msconfig.exe) を使用してブート設定を変更することもできます。
