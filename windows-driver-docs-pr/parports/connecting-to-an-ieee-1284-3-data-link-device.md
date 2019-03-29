---
title: IEEE 1284.3 データ リンク デバイスへの接続
description: IEEE 1284.3 データ リンク デバイスへの接続
ms.assetid: 306ff7db-472b-400a-8f14-3f7667160ded
keywords:
- パラレル ポート WDK、IEEE 1284 デバイス
- IEEE 1284 WDK
- データ リンク サービスのサポートの WDK パラレル ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4760b4a5536125b96a149bf33378c82b2368b2b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573035"
---
# <a name="connecting-to-an-ieee-12843-data-link-device"></a>IEEE 1284.3 データ リンク デバイスへの接続





パラレル ポートのシステムによって提供される関数のドライバーでは IEEE 1284.3 データ リンク層サービスの完全なサポートはされていませんただし、内部デバイスの制御が要求された上位のドライバーは、接続、切断、リセット、および IEEE 1284.3 データ リンク デバイスの通知を使用できますが提供されます。 これらのサービスでは、開発中はおり、一般利用可能な新しいデバイスをサポートするものです。 IEEE 1284.3 データ リンク サービスのサポートの詳細については、サンプル コードを参照してください。  *\\src\\カーネル\\parport* Microsoft Windows ドライバー開発キット (DDK) にします。 (前に、DDK、Windows Driver Kit \[WDK\])。

 

 




