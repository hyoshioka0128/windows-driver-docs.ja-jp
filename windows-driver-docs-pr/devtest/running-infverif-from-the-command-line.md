---
title: コマンドラインからの InfVerif の実行
description: このトピックでは、コマンドラインから InfVerif.exe を実行するときに使用できるオプションを使用します。
ms.assetid: CC2DB624-FFEE-4049-ACE7-4A24B330BADB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2686122d1c695c1b99b691115c45289947ead84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579449"
---
# <a name="running-infverif-from-the-command-line"></a>コマンドラインからの InfVerif の実行


このトピックでは、コマンドラインから InfVerif.exe を実行するときに使用できるオプションを使用します。
> [!NOTE]
> InfVerif では、各結合されたパスとファイル名は 260 文字未満である必要がありますが必要です。

```
USAGE: InfVerif.exe [/v] [/u | /universal] [/k] [/info] [/stampinf] [/l <path>]
                    [/osver TargetOSVersion>] [/product <ias file>] <files>

/v
        Display verbose file logging details.

/k
        Reports errors for Windows Update submission. (mode)

/u
        Reports errors if INF is not Universal. (mode)

/info
        Displays INF summary information.

/stampinf
        Treat $ARCH$ as a valid architecture, to validate
        pre-stampinf files.

/l <path>
        An inline-annotated HTML version of each INF
        file will be placed in the <path>.

/osver <TargetOsVersion>
        Process the INF for a specific target OS.
        Formatting is the same as a Models section, i.e. NTAMD64.6.0
        Matches the TargetOSVersion you would use in a Models section name (see link below)

/product <ias file>
        Validates all include/needs directives against
        the product definition in the ias file.

<files>
        A space-separated list of INF files to analyze.
        Wildcards (*) may be used.

Only one mode option may be passed at a time.
```

例については*TargetOSVersion* 「解説」を参照してください、書式設定セクションの[INF 製造元セクション](../install/inf-manufacturer-section.md)します。

/Verbose オプションは、INF が有効かどうかを指定する出力に行を追加します。  特定の引数は、モードとしてタグ付けされて 1 つだけを渡す必要があります。

*Windows 10 バージョン 1703: の新機能*ヒント オプションは、INF の適用性を確認する方が便利です。  有効なアーキテクチャと最小 OS バージョンには、各サポートされているハードウェア ID を報告します。  OS のバージョンとアーキテクチャの間で INF の適用性を検証するのに、/info と/osver をまとめて使用できます。

