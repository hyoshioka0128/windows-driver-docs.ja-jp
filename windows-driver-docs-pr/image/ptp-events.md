---
title: PTP イベント
description: PTP イベント
ms.assetid: 69bbe1e1-46e7-4615-93ff-ecd640e7d56b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d90dec6990c76709d3f447c22de13859ee799815
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538394"
---
# <a name="ptp-events"></a>PTP イベント





応答を含むオブジェクトが追加または削除したときに、 **StoreAdded**または**StoreRemoved**イベント (標準ピマ 15740 で説明)、WIA イベントがトリガーされます。 WIA\_イベント\_項目\_オブジェクトを追加すると、作成済みのイベントが発生し、WIA\_イベント\_項目\_DELETED イベント オブジェクトが削除されたときに発生します。 (これらおよび他の WIA イベント識別子の説明については、Microsoft Windows SDK ドキュメントを参照してください)。PTP ドライバーでは、PTP の他のイベントを使用して、内部の構造を更新するが、これらのイベントは、アプリケーションには報告されません。 PTP ドライバーは、アプリケーションには、デバイスが開くときにのみイベントの監視に注意してください。

 

 




