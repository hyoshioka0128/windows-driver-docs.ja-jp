---
title: 1394 のサンプルと診断ツール
description: 1394 のサンプルと診断ツール
ms.assetid: e3ce71da-8c24-405b-b734-98a8c4f45e6b
keywords:
- サンプルの IEEE 1394 WDK バス
- 1394 WDK バス, サンプル
- 診断ツールの IEEE 1394 WDK バス
- 1394 WDK バス、診断ツール
- サンプル ドライバー WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca81ef6ad9e515ed8600a700a4ab664853d04346
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376711"
---
# <a name="1394-samples-and-diagnostic-tools"></a>1394 のサンプルと診断ツール


Windows Driver Kit (WDK) には、2 つのサンプルのカーネル モード ドライバーのソース コードが含まれています (*1394vdev.sys*と*1394diag.sys*) と通信するためにドライバー作成者を許可する診断ソフトウェア、ユーザー モードからの IEEE 1394 スタックです。

ドライバーのソース コードは、IEEE 1394 スタックの上端とのドライバーの通信する方法を示しています。 だけでなく、非同期および isochronous データ転送は、サンプルのソース コードは、プラグ アンド プレイ (PnP) を適切に管理および電源管理 I/O 要求パケット (Irp) を示します。

システムを列挙*1394vdev.sys*と*1394diag.sys*が異なります。 1394vdev.sys ドライバーは、IOCTL を受信したときに、IEEE 1394 バス ドライバーが読み込まれる仮想診断ドライバー\_IEEE1394\_API\_要求。 *1394diag.sys*ドライバーは、IEEE 1394 のハードウェア デバイスを PC に接続したときに、IEEE 1394 バス ドライバーが読み込まれる物理診断デバイス ドライバー。 *1394vdev.inf*、これらのドライバーの両方を読み込み、WDK に含まれます。

 

 




