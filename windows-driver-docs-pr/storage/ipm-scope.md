---
title: IPM 適用範囲
description: IPM 適用範囲
ms.assetid: fa34f703-ab02-4a0d-96ae-e7cb89756992
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 021d0914aedea0a196bf90d558c870ae35dca5b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325292"
---
# <a name="ipm-scope"></a>IPM 適用範囲


Storport アイドル状態の電源管理 (IPM) は、アダプターではなく、LUN のアイドル状態の電源管理を提供します。 Storport IPM は、すべての Lun が省電力状態にある場合は、低電力状態に、アダプターを配置しません。 ミニポート ドライバーはアダプターの電源管理を担当します。

Storport IPM は次のシステム構成のみでサポートされています。

SATA アダプターを使用して、接続されている 1 台の SATA ディスク ドライブでシステム

Storport IPM は次のシステム構成ではサポートされていません。

アタッチされたストレージを (FC、iSCSI、およびその他のユーザー) は、direct 以外のシステム

外部ストレージ アレイと RAID コント ローラーのあるシステム

MPIO を搭載したシステム

SATA 以外のシステムのホスト バス アダプター

SATA アダプターに接続されている 1 つ以上のディスクを搭載したシステム

 

 




