---
title: トレース メッセージ コントロール ファイル
description: トレース メッセージ コントロール ファイル
ms.assetid: 4904a1d2-1314-49ad-bd57-ec976b18de13
keywords:
- トレース メッセージの制御ファイル WDK
- TMC ファイル WDK
- ファイルの WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7809e05e07808a1fb948a13109fe678d815422c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380482"
---
# <a name="trace-message-control-file"></a>トレース メッセージ コントロール ファイル


**注**  Windows Vista では、前に、この種類のファイルが既定で生成された[Tracepdb](tracepdb.md)します。 代わりに、Tracepdb ツールは、バイナリでプロバイダーの情報について説明します MOF (.mof) ファイルを生成するようになりました。
使用している場合を除き、 [traceview で](traceview.md)、これらの TMC ファイルへの参照を無視する必要があります。

 

A*トレースを制御するメッセージ*(TMC) ファイルを含むテキスト ファイルでは、[コントロール GUID](control-guid.md)各[トレース プロバイダー](trace-provider.md) PDB ファイルで表されます。 TMC ファイルの名前は、コントロールに .tmc ファイル名拡張子、トレース プロバイダーの GUID です。

[Tracefmt](tracefmt.md)と[traceview で](traceview.md)作成するときに、各トレース プロバイダーの TMC ファイルを作成、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)PDB ファイルの書式設定の指示をします。 [Tracepdb](tracepdb.md)を使用する場合も、TMC ファイルを生成できる、 **-c**オプション。

TMC ファイルには、次の情報も含まれています。

-   PDB ファイルのパスとファイル名。

-   日付と PDB ファイルが作成された時刻。

-   トレース プロバイダーごとにコントロールの GUID。

-   [トレース フラグ](trace-flags.md)トレース プロバイダーによって定義されています。

Traceview では、各プロバイダーのトレース フラグを検索するのに TMC ファイルを使用します。 このファイルは、コントロールのトレース プロバイダーの GUID のクイック リファレンスとして使用することができます。

 

 





