---
title: 拡張記憶域証明書の管理ツールのインストール
description: 拡張記憶域証明書の管理ツールのインストール
ms.assetid: 1494a911-73a4-4a8c-a29d-aecb65c846dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c07f5baa2d88d3cd9ecd4453195721fc6f6947f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560031"
---
# <a name="installation-of-the-enhanced-storage-certificate-management-tool"></a>拡張記憶域証明書の管理ツールのインストール


記憶域証明書の管理の強化されたツールは Windows 7 および Windows の以降のバージョンを実行する x86 ベース、Itanium ベースおよび x64 ベースのコンピューター。 コンピューターで、記憶域証明書の管理の強化されたツールをインストールするには、次の手順を完了します。

1.  WDKPath から EhStorCertMgrCmd.exe をコピー\\ツール\\EnhancedStorage\\%systemroot% ProcessorArchitecture\\System32 コンピューターの場所。

    -   *WDKPath* Windows Driver Kit (WDK) にインストールしたディレクトリのパスです。
    -   *ProcessorArchitecture*はコンピューターの記憶域証明書の管理の強化されたツールをインストールすることや実行されているのプロセッサ アーキテクチャです。 WDK ツールで、ファイルのプロセッサ固有バージョンをインストールする\\EnhancedStorage\\amd64、ツール\\EnhancedStorage\\i386、およびツール\\EnhancedStorage\\ia64下のサブディレクトリ、 *WDKPath*ディレクトリ。

    たとえば、テスト コンピューターで Windows の 32 ビット バージョンが実行されている場合があるツールをコピーする\\EnhancedStorage\\i386\\%systemroot% EhStorCertMgrCmd.exe\\System32 します。

2.  WDKPath から EhStorCertMgrComponent.dll をコピー\\ツール\\EnhancedStorage\\%systemroot% ProcessorArchitecture\\コンピューターの System32 します。

3.  EhStorCertMgrCmd.exe.mui および EhStorCertMgrComponent.dll.mui WDKPath からコピー\\ツール\\EnhancedStorage\\%systemroot% 内のロケール固有のサブディレクトリに ProcessorArchitecture\\の System32コンピューター。

    など、ロケールがアメリカ合衆国の場合は、する必要がありますすべてコピー .mui ファイルの %systemroot%\\System32\\EN-US (英語)。

4.  **[開始]** をクリックします。

5.  右クリック**コマンド プロンプト**クリック**管理者として実行**します。

6.  コマンド プロンプトで次のコマンドを入力します。
    ```
    regsvr32 /s %SystemRoot%/System32/EhStorCertMgrComponent.dll
    ```

**注**  拡張記憶域証明書管理ツールのファイルをコピーおよびインストールされている、WDK を持たない他のコンピューターにインストールされていることができます。

 

 

 





