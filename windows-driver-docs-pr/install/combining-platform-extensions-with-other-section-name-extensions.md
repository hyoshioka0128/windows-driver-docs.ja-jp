---
title: プラットフォーム拡張機能とその他のセクション名の拡張機能を組み合わせる
description: プラットフォーム拡張機能とその他のセクション名の拡張機能を組み合わせる
ms.assetid: ca82ba0f-0d65-47ca-826a-4f78435b1442
keywords:
- INF ファイル WDK デバイスのインストール、プラットフォーム拡張機能
- プラットフォーム拡張機能の WDK INF ファイル
- 拡張機能の WDK INF プラットフォーム
- プラットフォーム拡張機能と WDK INF ファイルの組み合わせ
- install-section-WDK INF ファイル名
- 装飾のある INF WDK
- オペレーティングシステム WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7361665e62800bc87330613afea8b435d9eb2af8
ms.sourcegitcommit: 53565c07d980307b079a6accf541fd221e623142
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86972153"
---
# <a name="combining-platform-extensions-with-other-section-name-extensions"></a>プラットフォーム拡張機能とその他のセクション名の拡張機能を組み合わせる


Inf *ddinstall*セクションとプラットフォーム拡張機能を含む inf ファイルには、必要な<em>ddinstall</em>など、デバイスごとの追加のセクションを含めることもでき**ます。サービス**とオプションの<em>ddinstall</em>**。HW**、 <em>ddinstall</em>**。CoInstallers**、 <em>ddinstall</em>**。LogConfigOverride**および<em>ddinstall</em>**。インターフェイス**セクション。 クロスオペレーティングシステムとクロスプラットフォームの INF ファイルでは、INF ライターで定義されたセクション名の直後に適切なプラットフォーム拡張機能を指定する必要が<em>あります (たとえば、</em>ntx86 を指定し**ます。ハードウェア**)。

クロスオペレーティングシステムの INF ファイルに装飾され<em>たインストールセクション名</em>**. nt**、**ntx86** <em>、</em>**ntia64** <em>、または</em>**ntamd64**セクションが含まれている場合は、さらに、追加の並列装飾および非装飾のデバイスごとのセクションも必要に<em>なります。</em> つまり、INF ファイルに*インストールセクション名*とインストールセクション名の両方の<em>install-section-name</em>**セクションが**あり、 *ddinstall*があるとします。**HW**セクションでは、並列<em>インストールセクション名</em>**. nt も必要です。HW**セクション (デバイスまたはドライバーにが必要な場合) **。** Windows 2000 以降のバージョンの windows の場合は、HW セクションを参照してください。

「 [INF ファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)」セクションのトピックでは、 **nt**<em>xxx</em>を示して**います。** 次の例のように、適切なセクション参照に含まれる正式な構文ステートメントの一部としての HW 拡張。

```inf
[install-section-name.HW] | 
[install-section-name.nt.HW] | 
[install-section-name.ntx86.HW] | 
[install-section-name.ntia64.HW] | 
[install-section-name.ntamd64.HW] 
```

このような正式な構文ステートメントは、これらの拡張機能が基本セクションの代替として有効であることを示します。 この種類のステートメントでは、<em>インストールセクション名</em>. nt を含む INF ファイルは指定*されていません***。HW**セクションには、プラットフォーム固有のその他すべての<em>インストールセクション名</em>**. nt**<em>xxx</em>も含まれている必要があります。**HW**セクション。 これらの拡張機能のサブセットを使用して、特定のクロスプラットフォームインストールに必要な装飾されたセクションを指定できます。

また、*インストール-セクション名*のプラットフォーム拡張機能を含む inf ファイルには、プラットフォーム固有の方法でインストールファイルの場所を指定するために、 [**Inf SourceDisksNames セクション**](inf-sourcedisksnames-section.md)と[**inf sourcedisksnames セクション**](inf-sourcedisksfiles-section.md)エントリを含むプラットフォーム拡張機能を含めることもできます。

