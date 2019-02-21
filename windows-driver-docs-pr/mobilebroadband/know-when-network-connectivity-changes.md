---
title: ネットワーク接続が変更されたときを知る
description: ネットワーク接続が変更されたときを知る
ms.assetid: 2937ba62-16ad-4a81-92e8-62a8bb40d608
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2108c211cedb431d3f76b2a3eb19f993a8997813
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538877"
---
# <a name="know-when-network-connectivity-changes"></a>ネットワーク接続が変更されたときを知る


ネットワーク接続の変更、使用時に知って、 [ **AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)のイベント[ **MobileBroadbandAccountWatcher**](https://msdn.microsoft.com/library/windows/apps/hh770597):

1.  インスタンスを作成、 [ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)オブジェクト。

2.  追加、 [ **AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)イベント ハンドラー。

3.  呼び出す[**開始**](https://msdn.microsoft.com/library/windows/apps/hh770604)ウォッチャーにします。

4.  クエリ、 [ **HasNetworkChanged** ](https://msdn.microsoft.com/library/windows/apps/hh770595)のプロパティ、 [ **MobileBroadbandAccountUpdatedEventArgs** ](https://msdn.microsoft.com/library/windows/apps/hh770593)オブジェクト、 [**AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)イベント ハンドラー。

5.  ネットワークが変更された場合は、クエリ、 [ **CurrentNetwork** ](https://msdn.microsoft.com/library/windows/apps/hh770610)現在のネットワーク オブジェクトのプロパティ。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






