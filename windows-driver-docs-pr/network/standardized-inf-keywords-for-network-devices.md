---
title: ネットワーク デバイス用の標準化された INF キーワード
description: ネットワーク デバイス用の標準化された INF キーワード
ms.assetid: F79AFB63-D404-4A5C-9515-82FFEB667048
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09f77d3d5cde454777adb118e73360ea4ea0fb70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841846"
---
# <a name="standardized-inf-keywords-for-network-devices"></a>ネットワーク デバイス用の標準化された INF キーワード





ここでは、レジストリに表示される標準化されたキーワードと、INF ファイルで指定されている情報について説明します。 Ndis 6.0 以降のバージョンの NDIS では、ネットワークデバイスのミニポートドライバーの標準化されたキーワードがサポートされています。

標準化されたキーワードは次のとおりです。

-   エンドユーザー向けの標準化されたユーザーインターフェイスプロパティ。

-   ホームネットワークユーザーと大規模企業の両方が、複数のハードウェア製造元のデバイスを含むネットワークを簡単に構成できます。

-   すべての高度なネットワークデバイス機能をプログラムによってテストする機能。

次の標準 INF キーワードは、コネクションレス NDIS 6.0 およびそれ以降のミニポートドライバーに必須です。

-   **\*IfType**

-   **\*MediaType**

-   **\*PhysicalMediaType**

必須キーワードがドライバーの INF ファイルにない場合、NDIS はミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出しません。

次の両方に該当する場合、NDIS 6.0 以降のミニポートドライバーには標準化されたキーワードが必要です。

-   INF 設定は、ユーザーインターフェイスの **[詳細**プロパティ] ページで公開する必要があります。

-   デバイスは、指定されたプロパティを完全にサポートしています。

**注**  標準化されたキーワードは省略可能ですが、ndis 5.1 およびそれ以前の ndis ミニポートドライバーでは推奨されています。

 

このセクションでは、ユーザーインターフェイスで公開されている INF キーワードを指定します。 ただし、ミニポートドライバーは、初期化中にレジストリ設定を読み取って、現在の構成設定を確認する必要があります。

INF ファイル内では、これらのキーワードの定義は、[詳細プロパティ] ページの他の定義と共に配置されます。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

すべての標準化されたキーワード名は、アスタリスク ( **\*** ) で始まります。 この名前付け規則を使用すると、標準以外の名前から標準化された名前を簡単に区別できます。

ユーザーインターフェイスで公開される標準化されたキーワードデータには、次の3種類があります。

<a href="" id="enum"></a>Enum  
**[詳細**プロパティ] ページのドロップダウンメニューに表示される一覧から選択できる値。

<a href="" id="int"></a>通り  
編集できる数値。

<a href="" id="edit"></a>編集  
編集できるテキスト値。

次のトピックには、すべてのネットワークテクノロジに共通する標準化されたキーワードの説明が含まれています。

[列挙型キーワード](enumeration-keywords.md)

[編集できるキーワード](keywords-that-can-be-edited.md)

[ユーザーインターフェイスに表示されないキーワード](keywords-not-displayed-in-the-user-interface.md)

また、次のトピックでは、ネットワークテクノロジに固有の標準化されたキーワードについて説明します。

[フィルタードライバーの INF ファイル設定](inf-file-settings-for-filter-drivers.md)

[NDKPI の INF 要件](inf-requirements-for-ndkpi.md)

[MB ミニポートドライバー INF 要件](mb-miniport-driver-inf-requirements.md)

[ヘッダーデータを分割するための標準化された INF キーワード](standardized-inf-keywords-for-header-data-split.md)

[NDIS Quality Service (QoS) の標準化された INF キーワード](standardized-inf-keywords-for-ndis-qos.md)

[NDIS 選択的中断の標準化された INF キーワード](standardized-inf-keywords-for-ndis-selective-suspend.md)

[NVGRE タスクオフロード用の標準化された INF キーワード](standardized-inf-keywords-for-nvgre-task-offload.md)

[パケット合体用の標準化された INF キーワード](standardized-inf-keywords-for-packet-coalescing.md)

[電源管理用の標準化された INF キーワード](standardized-inf-keywords-for-power-management.md)

[RSC 用の標準化された INF キーワード](standardized-inf-keywords-for-rsc.md)

[RSS 用の標準化された INF キーワード](standardized-inf-keywords-for-rss.md)

[シングルルート i/o 仮想化 (SR-IOV) 用の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)

[仮想マシンキュー用の標準化された INF キーワード (VMQ)](standardized-inf-keywords-for-vmq.md)

 

 





