---
title: 仮想関数のリソースの解放
description: 仮想関数のリソースの解放
ms.assetid: 48FACA22-69B2-456C-9009-3CA42DE94FC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a34d0c51cf079831422c68a116db6676e937da97
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356286"
---
# <a name="freeing-resources-for-a-virtual-function"></a>仮想関数のリソースの解放


上にあるドライバー要求リソース割り当ての PCI Express (PCIe) 仮想機能 (VF) のオブジェクト識別子 (OID) メソッドの要求を通じた[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf). 上にあるドライバーがの OID セット要求を使用したリソースを解放 VF リソースが正常に割り当てられた後、 [OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)します。

ここでは、次のトピックについて説明します。

[OID の発行\_NIC\_スイッチ\_FREE\_VF 要求](issuing-oid-nic-switch-allocate-vf-requests.md)

[OID の処理\_NIC\_スイッチ\_FREE\_VF 要求](handling-oid-nic-switch-allocate-vf-requests.md)

 

 





