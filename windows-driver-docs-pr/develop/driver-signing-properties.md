---
ms.assetid: A1DE1065-9D8F-405F-9807-5F0D3BE6F0AC
title: ドライバーの署名のプロパティ
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa3d8b39490757d3ec01d31670cca8a322f4894d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518606"
---
# <a name="driver-signing-properties"></a>ドライバーの署名のプロパティ

ソリューション エクスプローラーでプロジェクトを選択すると、**[Driver Signing (ドライバーの署名)]** ノードの **[プロパティ]** ダイアログに 2 つのプロパティ セクションが表示されます。

## <a name="span-idundergeneralspanspan-idundergeneralspanspan-idundergeneralspanunder-general"></a><span id="Under_General_"></span><span id="under_general_"></span><span id="UNDER_GENERAL_"></span>General (全般):


**Sign Mode (署名モード)**

-   **[Test Sign]** (テスト署名): Microsoft Visual Studio で、**[Test Certificate]** (テスト証明書) で指定されたテスト証明書を使ってドライバーに署名する必要があります (既定)。 **[Test Certificate]** (テスト証明書) で証明書が指定されていない場合は、ドライバー用に証明書が作成されます。 **注意**:Windows では、すべての 64 ビット ドライバーに署名が必要です。
-   **[Production Sign (実稼働署名)]** - Visual Studio で、**[Production Certificate (実稼働証明書)]** で指定された実稼働証明書を使ってドライバーに署名する必要があります。
-   **[オフ]** - Visual Studio で、証明書を使ってドライバーに署名できません。

**Test Certificate (テスト証明書)**

-   *空白* - テスト証明書が選択されていません (既定)。
-   **[&lt;編集...&gt;]** - **[Sign Mode]\(署名モード\)** が **[Test Sign]\(テスト署名\)** に設定されているときに使う証明書を選びます。

**Production Certificate (運用証明書)**

-   *空白* - 実稼働証明書が選択されていません (既定)。
-   **[&lt;編集...&gt;]** - **[Sign Mode]\(署名モード\)** が **[Production Sign]\(運用署名\)** に設定されているときに使う証明書を選びます。

**TimeStampServer (TimeStampServer)**

-   **[Verisign]** - ドライバーへのタイム スタンプの設定に VeriSign を使います (既定)。
-   **[GlobalSign]** - ドライバーへのタイム スタンプの設定に GlobalSign を使います。
-   **[なし]** - ドライバーにタイム スタンプを設定しません。

**Disable Warnings (警告の無効化)**

-   **[いいえ]** - ドライバーへの署名時に警告を表示します (既定)。
-   **[はい]** - ドライバーへの署名時に警告を表示しません。

**Enable Diagnostic Verbosity (診断の詳細度の有効化)**

-   **[いいえ]** - ドライバーへの署名時に診断の詳細度を表示しません (既定)。
-   **[はい]** - ドライバーへの署名時に診断の詳細度を表示します。

**File Digest Algorithm (ファイル ダイジェスト アルゴリズム)**

-   *空白* - ファイル ダイジェスト アルゴリズムが選択されていません (既定)。
-   **[&lt;編集...&gt;]** - ドライバーへの署名時に使うファイル ダイジェスト アルゴリズムを選びます。

## <a name="span-idundercommandlinespanspan-idundercommandlinespanspan-idundercommandlinespanunder-command-line"></a><span id="Under_Command_Line_"></span><span id="under_command_line_"></span><span id="UNDER_COMMAND_LINE_"></span>Command Line (コマンド ライン):


**Additional Options (追加オプション)**

-   ドライバーへの署名時に指定する追加オプション。

 

 





