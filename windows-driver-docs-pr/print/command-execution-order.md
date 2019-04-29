---
title: コマンド実行順序
description: コマンド実行順序
ms.assetid: 2bf7438c-bfb0-407f-9c80-be3b8a9322f9
keywords:
- プリンターの WDK Unidrv、実行順序コマンドします。
- シーケンス番号の WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 950bc0c7bc784778d077f5e298d3901ea8b5754f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392889"
---
# <a name="command-execution-order"></a>コマンド実行順序





プリンターのコマンドは、意味のある順序でプリンターのハードウェアに送信する必要があります。 Unidrv には、GPD 言語で定義されているコマンド名のほとんどは、コマンドのエスケープ シーケンスをプリンターに送信されるタイミングを認識しています。 2 つの例外があります。

[選択コマンドのオプション](option-selection-command.md)

[プリンター構成コマンド](printer-configuration-commands.md)

これらのコマンドの種類の両方のコマンドの実行順序を指定する必要があります。

コマンドの実行順序は--をジョブ セクションの名前とシーケンス番号を 2 つのコンポーネントの構成されます。 Unidrv ドライバーでは、各印刷ジョブを 6 つのセクションに分割します。 各セクションでは、Unidrv によって、セクションを指定したシーケンスに割り当てられているコマンドがプリンターに送信します。 次のセクションが定義されています。

<a href="" id="job-setup"></a>ジョブ\_セットアップ  
ジョブに割り当てられているコマンド\_ジョブごとのセットアップ セクションが 1 回送信されます。 新しいジョブの開始時に送信される最初のコマンドが表示されます。 これらのコマンドは、の Unidrv の実装内から送信される、 [ **DrvStartDoc** ](https://msdn.microsoft.com/library/windows/hardware/ff556296)関数。

<a href="" id="doc-setup"></a>DOC\_セットアップ  
ドキュメントに割り当てられているコマンド\_設定」のセクションは、ドキュメントの最初のページが送信される前に送信されます。 コマンドは、DrvStartDoc 関数の Unidrv の実装内からを送信されます。 (これらのコマンドも送信後、アプリケーションが Win32 印刷関数を呼び出します。 このセクションのコマンドで削除しないでダウンロードについては、ソフト フォントやパターンなど。)

<a href="" id="page-setup"></a>ページ\_セットアップ  
ページに割り当てられているコマンド\_設定」のセクションは、描画を開始する前に、新しい各ページの先頭に送信されます。 これらのコマンドは、の Unidrv の実装内から送信される、 [ **DrvStartPage** ](https://msdn.microsoft.com/library/windows/hardware/ff556298)関数。

<a href="" id="page-finish"></a>ページ\_完了  
ページに割り当てられているコマンド\_描画が完了したら、[完了] セクションが、各ページの最後に送信されます。 これらのコマンドは、の Unidrv の実装内から送信される、 [ *DrvSendPage* ](https://msdn.microsoft.com/library/windows/hardware/ff556281)関数。

<a href="" id="doc-finish"></a>DOC\_完了  
ドキュメントに割り当てられているコマンド\_ドキュメントの最後のページが送信された後、[完了] のセクションは送信されます。 コマンドは、の Unidrv の実装内から送信される、 [ **DrvEndDoc** ](https://msdn.microsoft.com/library/windows/hardware/ff556215)関数。 (このセクションのコマンドでは、ソフト フォントやパターンなど、ダウンロードした情報を削除する必要がありますされません)。

<a href="" id="job-finish"></a>ジョブ\_完了  
ジョブに割り当てられているコマンド\_[完了] のセクションでは、ジョブごと 1 回送信されます。 ジョブの終了時に送信された最後のコマンドが表示されます。 これらのコマンドは、DrvEndDoc 関数の Unidrv の実装内からを送信されます。

各セクション内では、コマンドは、シーケンス番号によって示される順序で実行されます。

コマンドのセクションとシーケンス番号を指定するには、使用、 **\*順序**属性に説明されている、[コマンド属性](command-attributes.md)します。 形式です。

**\*順序**:*SectionName*.*SequenceNumber*

場所*SectionName*はジョブの 1 つ\_セットアップ、DOC\_セットアップ ページ\_セットアップ ページ\_[完了]、ドキュメント\_[完了]、またはジョブ\_完了と*SequenceNumber*は数値です。

シーケンス番号を連続している必要はありませんが、セクション内で指定された各番号は一意である必要があります。 セクション内のコマンドは、最高の最小のシーケンス番号を持つ 1 つから実行されます。 たとえば、次のエントリを示すオプションを**InputBin**、 **PaperSize**、および**解決**機能は、ドキュメントに割り当てられている\_セットアップセクションとは、指定した順序で送信されます。

```cpp
*Feature: InputBin
{
    *Option: Auto
    {
        *Name: "Auto Tray"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.50
            *Cmd: "<1B>(1<010014>"
        }
    }
    ...
}
*Feature: PaperSize
{
    *DefaultOption: Letter
    *Option: Letter
    {
        *Name: "Letter size"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.60
            *Cmd: "<1B>(g<0300>n<01>r"
        }
    }
    ...
}
*Feature: Resolution
{
    *DefaultOption: 360dpi
    *Option: 360dpi
    {
        *Name: "360 dpi x 360dpi"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.70
            *Cmd: "<1B>(d<020001>"
        }
    }
    ...
}
```

 

 




