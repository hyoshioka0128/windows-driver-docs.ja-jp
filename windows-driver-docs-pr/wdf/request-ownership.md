---
title: 要求の所有権
description: 要求の所有権
ms.assetid: 60494e97-0483-454f-aafc-7a69019c95f2
keywords:
- WDK KMDF、所有権の要求オブジェクト
- WDK KMDF、所有権 I/O 要求します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30885d929be0f951588069a7b951974eecce39ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580177"
---
# <a name="request-ownership"></a>要求の所有権


I/O マネージャーでは、framework ベースのドライバーに、I/O 要求を送信するときにフレームワークが要求を受信し、framework 要求オブジェクトを作成します。 フレームワーク"所有"する要求オブジェクト、framework のみがアクセス要求と、オブジェクトに対して操作を実行するためです。

フレームワークには、要求オブジェクトが作成された後、ドライバーの I/O キューのいずれかで、オブジェクトを配置します。 フレームワークは、要求がキューから削除し、ドライバーに配信されるまで、要求オブジェクトを所有し続けます。

ドライバーの後に[受信](receiving-i-o-requests.md)要求オブジェクトを要求を所有しています。 ドライバーでは、要求オブジェクトのハンドルを使用してアクセスでき、オブジェクトの操作を実行することができます。 可能なドライバーは、要求オブジェクトを所有しているときに[requeue](requeuing-i-o-requests.md)、[完了](completing-i-o-requests.md)、[キャンセル](canceling-i-o-requests.md)、または[フォワード](forwarding-i-o-requests.md)その不要になった後、要求要求オブジェクトを所有し、アクセスできません。

要求オブジェクトの所有権は、ドライバー、フレームワークの間で通過、オブジェクト ハンドルの値は変更されません。 たとえば、ドライバーは、I/O キューから要求を受信し、別のキューにキューに再登録がもう一度要求を受信し場合、このハンドルの値は変更されません。 同様に、ドライバーは、I/O のターゲットに要求を転送し、後で I/O の対象に、要求が完了したことの通知を受け取る、ドライバーの通知のコールバック関数は、ドライバーは、I/O のターゲットに指定されたハンドル値と同じ値を受け取ります。

 

 





