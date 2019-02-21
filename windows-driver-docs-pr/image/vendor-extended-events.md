---
title: ベンダー拡張イベント
description: ベンダー拡張イベント
ms.assetid: 00131b75-3b15-46f8-b4da-1e1593afb3c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56633f19d0b82b1f2a2db7d3078e1ead510555d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553709"
---
# <a name="vendor-extended-events"></a>ベンダー拡張イベント





ベンダー拡張イベントがで定義されている、 **DeviceData**と**イベント**INF ファイルのセクション (例を参照してください。 [Vendor-Extended 機能](vendor-extended-features.md))。 **EventCode**エントリは、コンマで区切られたのすべてのイベント コードを一覧表示されます。 各イベントのコード、フォームのエントリの **EventCode * * * XXXX* XXXX が大文字の 16 進数で PTP イベント コードは、存在する必要があります。 エントリには、ドライバーを示すイベント コードを受信したときに送信する WIA GUID コードが一覧表示します。

イベントの表示名を宣言する必要があります、**イベント**セクション。 各イベントに対して、必要があります、**EventCode * * * XXXX*コンマで区切られたすべて引用符、GUID、イベントおよびイベントの発生時に起動するアプリケーションで、イベント名を含むエントリ。 アプリケーション名の代わりにアスタリスクを使用する場合は、登録済みのアプリケーション名が使用されます。 参照してください[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)詳細についてはします。 アプリケーションで使用できます、**IWiaDevMgr::RegisterEventCallback * * * Xxx*メソッド (Microsoft Windows SDK のドキュメントで説明)、イベントを受信します。 現時点では、イベントからのパラメーターは、アプリケーションに渡すことはできません。

 

 




