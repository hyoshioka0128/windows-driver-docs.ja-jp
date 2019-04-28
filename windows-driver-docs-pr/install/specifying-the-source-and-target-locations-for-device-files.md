---
title: デバイス ファイルのソースとターゲットの場所の指定
description: デバイス ファイルのソースとターゲットの場所の指定
ms.assetid: e44961e2-e9fb-43d3-aeb9-a625021e56e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59d25c19b848862a069ff4f8cd13d9649db4fd58
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369404"
---
# <a name="specifying-the-source-and-target-locations-for-device-files"></a>デバイス ファイルのソースとターゲットの場所の指定





Windows プロセスは、コピー、名前の変更、および、INF ファイルでステートメントをファイルの削除、ときに、ファイルのソースとターゲットの場所を決定します。 これらの場所を決定するには、ドライバーはオペレーティング システムまたは個別に用意されていて、さまざまなファイルのセクションでは INF およびなどのエントリを調べかどうかを評価**SourceDisksNames**、 **SourceDisksFiles**、**含める**、**必要がある**、および**DestinationDirs**します。

Windows ソースを確認しますターゲットの場所、およびこれらの場所が正しく指定するためのガイドラインを提供しますおよび方法 1 つの場所からで INF ファイルをコピーする方法について説明しますについて説明します。 このガイドには、次のトピックがあります。

[ソース メディアの INF ファイル](source-media-for-inf-files.md)

[対象のメディアの INF ファイル](target-media-for-inf-files.md)

[INF ファイルのコピー](copying-inf-files.md)

 

 





