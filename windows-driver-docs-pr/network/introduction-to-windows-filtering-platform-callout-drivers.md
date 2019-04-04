---
title: Windows プラットフォームのコールアウト ドライバーをフィルタ リングの概要
description: Windows プラットフォームのコールアウト ドライバーをフィルタ リングの概要
ms.assetid: d075da82-8dbc-41a5-a081-dd0e2b292371
keywords:
- コールアウト ドライバーについてコールアウト ドライバー WDK、Windows フィルタ リング プラットフォーム
- コールアウト ドライバーの詳細については、コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
- コールアウト WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2eeb7b6039ef79ec6a95dfde477a70020ca6ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528101"
---
# <a name="introduction-to-windows-filtering-platform-callout-drivers"></a>Windows プラットフォームのコールアウト ドライバーをフィルタ リングの概要


ここでは Windows フィルタ リング プラットフォーム[コールアウト ドライバー](callout-driver.md)します。 Windows フィルタ リング プラットフォームの詳細については、次を参照してください。、 [Windows フィルタ リング プラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK のドキュメント。

### <a name="purpose-of-callout-drivers"></a>コールアウト ドライバーの目的

コールアウト ドライバーが 1 つ以上実装[コールアウト](callout.md)します。 コールアウトは、単純なフィルター機能の範囲外の方法での TCP ベースのネットワーク データを処理することによって Windows フィルタ リング プラットフォームの機能を拡張します。 コールアウトは、次のタスクを実行する通常使用されます。

<a href="" id="deep-inspection-------"></a>**詳細な検査**   
データをブロックするか、データにアクセスを許可する必要があります、およびデータを別のフィルターに渡す必要がありますを決定するネットワーク データの複雑な検査を実行します。 たとえば、ウイルス対策製品では、ウイルス シグネチャのなります可能性があります。

<a href="" id="packet-modification-------"></a>**パケットの変更**   
変更されていて、ネットワーク パケットのヘッダーまたはデータ、またはその両方の reinjection を実行します。 たとえば、ネットワーク アドレス変換 (NAT) 製品は、IPv4 パケットのヘッダーを変更できます。

<a href="" id="stream-modification-------"></a>**Stream の変更**   
ストリームで変更されていて、ネットワーク データの reinjection を実行します。 保護者製品では、たとえば、するまたは削除がデータ ストリームで特定の単語や語句を置き換える可能性があります。

<a href="" id="data-logging-------"></a>**データのログ記録**   
ネットワーク トラフィック データのログです。 などのネットワーク監視製品は、特定の理由で破棄されたデータ パケットの数をカウントしてでした。

ネットワーク データを処理するには、だけでなく、コールアウト ドライバーは、ベース エンジンをフィルター処理にフィルターを追加するなど、他の Windows フィルタ リング プラットフォーム管理タスクを実行できます。 コールアウト ドライバーを実行できるその他のタスクの詳細については、[その他の Windows フィルタ リング プラットフォーム関数の呼び出し](calling-other-windows-filtering-platform-functions.md)を参照してください。

 

 





