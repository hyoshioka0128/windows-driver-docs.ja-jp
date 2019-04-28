---
title: PTP イベント
description: PTP イベント
ms.assetid: 69bbe1e1-46e7-4615-93ff-ecd640e7d56b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d90dec6990c76709d3f447c22de13859ee799815
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379618"
---
# <a name="ptp-events"></a>PTP イベント





応答を含むオブジェクトが追加または削除したときに、 **StoreAdded**または**StoreRemoved**イベント (標準ピマ 15740 で説明)、WIA イベントがトリガーされます。 WIA\_イベント\_項目\_オブジェクトを追加すると、作成済みのイベントが発生し、WIA\_イベント\_項目\_DELETED イベント オブジェクトが削除されたときに発生します。 (これらおよび他の WIA イベント識別子の説明については、Microsoft Windows SDK ドキュメントを参照してください)。PTP ドライバーでは、PTP の他のイベントを使用して、内部の構造を更新するが、これらのイベントは、アプリケーションには報告されません。 PTP ドライバーは、アプリケーションには、デバイスが開くときにのみイベントの監視に注意してください。

 

 




