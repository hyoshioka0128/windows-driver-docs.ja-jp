---
title: ネットワーク デバイス用の標準化された INF キーワード
description: ネットワーク デバイス用の標準化された INF キーワード
ms.assetid: F79AFB63-D404-4A5C-9515-82FFEB667048
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d55125e09c24d6b12248b4802e6a992ee71543a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345961"
---
# <a name="standardized-inf-keywords-for-network-devices"></a>ネットワーク デバイス用の標準化された INF キーワード





このセクションでは、レジストリにある、INF ファイルで指定されている標準のキーワードに関する情報を提供します。 NDIS 6.0 および以降のバージョンの NDIS ミニポートのドライバーをネットワーク デバイスの標準化されたキーワードをサポートします。

標準化されたキーワードを提供します。

-   エンドユーザーの標準化されたユーザー インターフェイスのプロパティです。

-   複数のハードウェア製造元からデバイスを含むネットワークを簡単に構成するホーム ネットワーク ユーザーと大規模な企業の両方の権限です。

-   プログラムですべて高度なネットワーク デバイスの機能をテストする機能。

次の標準の INF キーワード コネクションレスの NDIS 6.0 とそれ以降のミニポート ドライバーの必須のとおりです。

-   **\*IfType**

-   **\*メディアの種類**

-   **\*PhysicalMediaType**

NDIS ミニポート ドライバーの呼び出しません必須キーワードが、ドライバーの INF ファイルから不足している場合に、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

次の両方に該当する場合は、標準化されたキーワードを NDIS 6.0 とそれ以降のミニポート ドライバーの必要があります。

-   INF 設定を公開する必要があります、**詳細**ユーザー インターフェイスのプロパティ ページ。

-   デバイスは、指定したプロパティを完全にサポートします。

**注**  標準化されたキーワードは、省略可能ですが、NDIS 5.1 および以前の NDIS ミニポート ドライバーのことをお勧めします。

 

このセクションでは、ユーザー インターフェイスで公開されている INF キーワードを指定します。 ただし、ミニポート ドライバーでは、現在の構成設定を判断するために初期化中にレジストリ設定を読み取る必要があります。

INF ファイル内では、これらのキーワードの定義は、高度なプロパティ ページの他の定義に配置されます。 高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

キーワードは、アスタリスクで始まるを標準化すべて (* *\\* * *)。 この名前付け規則では、標準名の名前を標準化を簡単に区別することができます。

ユーザー インターフェイスで公開されているキーワードの標準化されたデータの 3 つの種類があります。

<a href="" id="enum"></a>列挙型  
ドロップダウン メニューに表示される一覧から選択できる値、**詳細**プロパティ ページ。

<a href="" id="int"></a>Int  
数値を編集することができます。

<a href="" id="edit"></a>編集します。  
編集可能なテキスト値。

次のトピックでは、すべてのネットワーク テクノロジに共通する標準化されたキーワードの説明のとおりです。

[列挙型のキーワード](enumeration-keywords.md)

[編集可能なキーワード](keywords-that-can-be-edited.md)

[ユーザー インターフェイスに表示されないキーワード](keywords-not-displayed-in-the-user-interface.md)

さらに、ネットワーク テクノロジに固有の標準的なキーワードは、次のトピックについて説明します。

[フィルター ドライバーの INF ファイルの設定](inf-file-settings-for-filter-drivers.md)

[NDKPI INF の要件](inf-requirements-for-ndkpi.md)

[MB ミニポート ドライバーの INF の要件](mb-miniport-driver-inf-requirements.md)

[ヘッダー データの分割の標準化された INF キーワード](standardized-inf-keywords-for-header-data-split.md)

[NDIS サービスの品質 (QoS) の標準化された INF キーワード](standardized-inf-keywords-for-ndis-qos.md)

[NDIS オプションを選択するための標準化された INF キーワードを中断します。](standardized-inf-keywords-for-ndis-selective-suspend.md)

[NVGRE タスク オフロード用の標準化された INF キーワード](standardized-inf-keywords-for-nvgre-task-offload.md)

[パケットの結合の標準化された INF キーワード](standardized-inf-keywords-for-packet-coalescing.md)

[電源管理のための標準化された INF キーワード](standardized-inf-keywords-for-power-management.md)

[RSC の標準化された INF キーワード](standardized-inf-keywords-for-rsc.md)

[RSS の標準化された INF キーワード](standardized-inf-keywords-for-rss.md)

[シングル ルート I/O 仮想化 (SR-IOV) の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)

[仮想マシン キュー (VMQ) の標準化された INF キーワード](standardized-inf-keywords-for-vmq.md)

 

 





