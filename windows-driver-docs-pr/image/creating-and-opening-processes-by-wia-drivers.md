---
title: WIA ドライバーによってプロセスを作成して開く
description: WIA ドライバーによってプロセスを作成して開く
ms.assetid: c939eb25-b92b-41ef-ade0-98c2a707fee6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab761149b2a01f55254b8fbc35feed1006842ea1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386314"
---
# <a name="creating-and-opening-processes-by-wia-drivers"></a>WIA ドライバーによってプロセスを作成して開く





WIA ドライバーでは、システムで他のプロセスを起動する必要があります。 この 2 つの最も重要な理由は次に示します。

1.  呼び出す**CreateProcess** (Microsoft Windows SDK のドキュメントで説明)、サービスが起動した同じアカウントでプロセスを開始します。 Windows xp の場合、これは、 **LocalSystem**重大なセキュリティ リスクであるアカウント。

2.  呼び出す**CreateProcessAsUser** (Windows SDK のドキュメントで説明)、ユーザーの切り替え (FUS) またはターミナル サービス (TS) 環境では難しい。 正しくこのレベルで実装されているコンポーネントに簡単に可能性がありますいない特権や情報漏えい攻撃のエスカレーションが成功します。

**LocalService**アカウントには他のプロセスを開始するのに十分な特権がありません。 そのため、Microsoft Windows Server 2003 以降で、WIA ドライバーは、プロセスを作成できません。

別のプロセスがデバイスの機能に必要な場合は、これが、システムのサービスまたはローカル COM サーバーとして実装することをお勧めします。 システム サービスと COM サーバーの作成に関連する特定のセキュリティ情報の Microsoft のドキュメントを参照してください。

 

 




