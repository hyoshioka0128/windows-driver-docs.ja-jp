---
title: 仮想関数のリソースの解放
description: 仮想関数のリソースの解放
ms.assetid: 48FACA22-69B2-456C-9009-3CA42DE94FC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 340a77abc2da974a4e0c12ed8bdfe9bddf0b58ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581398"
---
# <a name="freeing-resources-for-a-virtual-function"></a>仮想関数のリソースの解放


上にあるドライバー要求リソース割り当ての PCI Express (PCIe) 仮想機能 (VF) のオブジェクト識別子 (OID) メソッドの要求を通じた[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814). 上にあるドライバーがの OID セット要求を使用したリソースを解放 VF リソースが正常に割り当てられた後、 [OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)します。

ここでは、次のトピックについて説明します。

[OID の発行\_NIC\_スイッチ\_FREE\_VF 要求](issuing-oid-nic-switch-allocate-vf-requests.md)

[OID の処理\_NIC\_スイッチ\_FREE\_VF 要求](handling-oid-nic-switch-allocate-vf-requests.md)

 

 





