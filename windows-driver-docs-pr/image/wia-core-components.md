---
title: WIA Core コンポーネント
description: WIA Core コンポーネント
ms.assetid: 59c02fa2-9116-4b57-a8fa-b977a4d6c714
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: d4a708ad41ee58cd3143400e25df507a1f2789bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370044"
---
# <a name="wia-core-components"></a>WIA Core コンポーネント

WIA コンポーネントは、次の図に表示されます。

![wia コア コンポーネントを示す図](images/stiwhist.png)

WIA サービス (*wiaservc.dll*) と呼ばれる一般的なホストによってホストされている*svchost.exe*します。 *Wiaservc.dll*は 1 つまたは複数ユーザー モード静止イメージ ドライバー (ラベルの付いた USD1 USD2、および図に USD3) カーネル モード ドライバーの特定の型との通信と通信します。 Windows では、3 種類のバスの抽象化を提供します。USB、SCSI、およびシリアル ( *usbscan.sys*、 *scsiscan.sys*、および*serscan.sys*)。

クライアント側では、アプリケーションは、TWAIN と互換性のあるアプリケーションのいずれかを指定できます (を参照してください[TWAIN と互換性のあるアプリケーションのサポート](support-for-twain-compatible-applications.md)) または WIA アプリケーション。 TWAIN アプリケーションを呼び出してデータ ソースのマネージャーを呼び出す*wiadss.dll*のインスタンスと通信する平行移動成分*のみ*します。 *のみ*WIA サービスと通信するスタブします。 これに対し、呼び出しを行う WIA アプリケーションに直接*のみ*します。
