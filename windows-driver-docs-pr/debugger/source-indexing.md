---
title: ソースのインデックス作成
description: ソースのインデックス作成
ms.assetid: 381020c6-26b1-48ab-bc7d-9ab718ecb89f
keywords:
- ソースのインデックス作成
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b418ffcee52752657ba98ee3cc94b67f375ab63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368106"
---
# <a name="source-indexing"></a>ソースのインデックス作成


一般に、バイナリは、ソースにインデックス付けされたビルド プロセス中に、アプリケーションがビルドされます。 SrcSrv で必要な情報は、.pdb ファイルに格納されます。 SrcSrv には、次のソース管理システムが現在サポートされています。

-   Perforce

-   Microsoft Visual SourceSafe

-   Microsoft Team Foundation Server

さまざまなソース管理システム用のコードのインデックスを作成するカスタム スクリプトを作成することもできます。 Subversion のような 1 つのモジュールは、このパッケージに含まれます。

SrcSrv には、ソースのインデックス作成プロセスで使用される 5 つのツールが含まれています。

[Srcsrv.ini ファイル](the-srcsrv-ini-file.md)

[Ssindex.cmd スクリプト](the-ssindex-cmd-script.md)

[付けて SrcTool ユーティリティ](the-srctool-utility.md)

[PDBStr ツール](the-pdbstr-tool.md)

[VSSDump ツール](the-vssdump-tool.md)

これらのツールでは、サブディレクトリ srcsrv でツールを Windows のデバッグにインストールされ、SrcSrv と同じパスにインストールされたままにする必要があります。 これらのツールで、PERL スクリプトでは、PERL 5.6 以降が必要です。

 

 





