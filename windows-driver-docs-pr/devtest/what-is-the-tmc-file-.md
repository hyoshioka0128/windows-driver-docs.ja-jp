---
title: TMC ファイルとは
description: TMC ファイルとは
ms.assetid: 5927d6be-93af-4ab2-bdc1-387fabc9c5ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dc08066c02bae9e03673e22cb02916cbf7d2065
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379134"
---
# <a name="what-is-the-tmc-file"></a>TMC ファイルとは

> [!NOTE]
> 使用している場合を除き、 [traceview で](traceview.md)、これらの TMC ファイルへの参照を無視します。

[トレース メッセージのコントロール (.tmc) ファイル](trace-message-control-file.md)を含むテキスト ファイルには、[コントロール GUID](control-guid.md)の各トレース レベルと共に[トレース プロバイダー](trace-provider.md) で表される[PDB シンボル ファイル](pdb-symbol-files.md)します。 TMC ファイルの名前は、コントロールに .tmc ファイル名拡張子、トレース プロバイダーの GUID です。

[Traceview で](traceview.md)を作成するときに、TMC ファイルを生成、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)PDB シンボル ファイルから。 [Tracepdb](tracepdb.md)を使用する場合も、TMC ファイルを生成できる、 **-c**オプション。

トレースのほとんどのツールでは、TMC ファイルは使用しないで、traceview でのコントロールのトレース プロバイダーの GUID を関連付けるためにそれが使用で、[トレース フラグ](trace-flags.md)と[トレース レベル](trace-level.md)プロバイダーがサポートします。
