---
title: コマンドラインからの InfVerif の実行
description: このトピックでは、コマンドラインから InfVerif を実行するときに使用できるオプションの一覧を示します。
ms.assetid: CC2DB624-FFEE-4049-ACE7-4A24B330BADB
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8486fabd13756ad7fcc9eee3688f992988e7b8db
ms.sourcegitcommit: 4d1ed685d198629f792d287619621a87ca42c26f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435366"
---
# <a name="running-infverif-from-the-command-line"></a>コマンドラインからの InfVerif の実行


このトピックでは、コマンドラインから InfVerif を実行するときに使用できるオプションの一覧を示します。
> [!NOTE]
> InfVerif では、各パスとファイル名を260文字未満にする必要があります。

```
USAGE: InfVerif.exe [/v] [/u | /universal] [/w] [/k] [/info] [/stampinf] [/l <path>]
                    [/osver TargetOSVersion>] [/product <ias file>] <files>

/v
        Display verbose file logging details.

/k
        Reports errors for Windows Update submission. (mode)

/u
        Reports errors if INF is not Universal. (mode)

/w
        Reports Windows Driver compatibility. See below. (mode)

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

Verbose オプションは、INF が有効かどうかを指定する行を出力に追加します。  特定の引数はモードとしてタグ付けされ、1つだけを渡す必要があります。

*TargetOSVersion*書式設定の例については、「 [INF Manufacturer」セクション](../install/inf-manufacturer-section.md)の「解説」を参照してください。

*Windows 10 バージョン1703の新バージョン:* Info オプションは、INF の適用性を確認する場合に特に役立ちます。  サポートされている各ハードウェア ID と、有効なアーキテクチャおよび最小 OS バージョンを報告します。  /Info と/osver を一緒に使用して、OS のバージョンとアーキテクチャ全体で INF の適用性を検証することができます。

*Windows 10 バージョン1809の新バージョン:* *Windows ドライバー*を開発している場合は、(では) を使用して、 `infverif /w` `/v` [dch Design 原則](../develop/dch-principles-best-practices.md)の**宣言 (D)** の原則との互換性を判断します。  また、このフラグは、 `/w` INF が[Windows ドライバーとはじめに](../develop/getting-started-with-windows-drivers.md)の[ドライバーパッケージ分離](../develop/driver-isolation.md)要件に準拠しているかどうかも確認します。

複数の INF ファイルを検証するには、複数のファイル名を指定するか、ワイルドカードを使用します。

```
infverif.exe /w test1.inf test2.inf
infverif.exe /w test*.inf
```