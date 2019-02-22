---
title: NVGRE タスク オフロードの概要
description: Generic Routing Encapsulation (NVGRE) タスク オフロードを使用してネットワーク仮想化の概要について説明します
ms.assetid: 5890AF7E-93E1-4E19-B483-C75657D749EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3482ebacd55cc5044f568a945548cf1eaca966a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560681"
---
# <a name="overview-of-network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>Generic Routing Encapsulation (NVGRE) タスク オフロードを使用してネットワーク仮想化の概要


## <a name="nvgre-encapsulation-packet-format"></a>NVGRE カプセル化パケットの形式

ここでは、プロトコルまたはフィルター ドライバーでは、GRE カプセル化を含む、(非 LSO) パケットを生成し、ネットワーク上でパケットを送信します。 これら (非-RSS、VMQ)、受信側でのパケットは変更せず、プロトコル ドライバーに渡されます。 NVGRE タスク オフロード機能をカプセル化およびカプセル化解除操作のオフロードする指定がされていないことに注意してください。

## <a name="send-and-receive-offloads"></a>送信および受信の負荷を軽減

次のタスクは、送信パス上のカプセル化のアカウントに必要をオフロードします。

-   IPv4 と TCP または UDP ペイロードのチェックサムの計算
-   大規模な Send Offload バージョン 1 (LSO\_v1) とバージョン 2 の Large Send Offload (LSO\_v2)

送信側がオフロードのミニポートはトンネル (外側) の IP ヘッダー、トランスポート (内部) の IP ヘッダーと TCP ヘッダーに対応する操作を実行する必要があります。

受信パスでは、次のタスクは、カプセル化のアカウントに必要をオフロードします。

-   IPv4 と TCP または UDP ペイロードのチェックサムの検証
-   受信側 scaling (RSS)
-   VMQ

受信側のオフロード NIC は、カプセル化プロトコル ヘッダーを解析する必要があります。 たとえば、GRE のカプセル化の NIC する必要があります GRE ヘッダーを解析し、実行 (内部) トランスポートでの作業負荷やトンネル (外部) の IP ヘッダー。

 

 





