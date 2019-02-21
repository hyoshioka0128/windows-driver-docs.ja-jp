---
title: フロー制御
description: フロー制御
ms.assetid: e7a0846e-0999-4e40-83e0-f4877871f1e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 505340af4262ec8a8d789effdc41252b8a999f83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529072"
---
# <a name="flow-control"></a>フロー制御





リモートの NDIS の USB デバイスのフロー制御は、USB 仕様によって定義されます。

USB 上のすべての通信は、デバイスのトランザクションをホストに基づいているためホストは、データのフローを行う必要がありますすべては、一括パイプでデバイスへのトークンで発行を停止します。 デバイスは、フロー制御をアサートする必要がある場合は、ホストからのデータ転送の NAK がもう一度データを処理することになるまで。 このプロセスの詳細については、USB 仕様、バージョン 1.1 の 8.4.4」セクションを参照してください。

 

 





