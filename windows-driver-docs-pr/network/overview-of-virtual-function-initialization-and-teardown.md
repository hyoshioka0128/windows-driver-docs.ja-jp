---
title: 仮想関数の初期化と切断の概要
description: 仮想関数の初期化と切断の概要
ms.assetid: 2684A93A-40C2-49DA-925D-2BAACA9F8CD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e820d0fc55766f0bf410c49d9e858dc9f7555690
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570815"
---
# <a name="overview-of-virtual-function-initialization-and-teardown"></a>仮想関数の初期化と切断の概要


このセクションでは、PCI Express (PCIe) 仮想機能 (Vf) の初期化と破棄の順序の概要を示します。 VFs は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターによって提供されます。

ここでは、次のトピックについて説明します。

[仮想関数の初期化シーケンス](virtual-function-initialization-sequence.md)

[仮想関数の破棄順序](virtual-function-teardown-sequence.md)

SR-IOV 対応ネットワーク アダプターの VFs の詳細については、[SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)を参照してください。

**注**  だけで、PF ミニポート ドライバーは Vf などのネットワーク アダプターのハードウェア リソースを構成できます。 VF のミニポート ドライバーでは、SR-IOV 対応のアダプターのハードウェア リソースのほとんどを直接アクセスできません。 詳細については、[書き込み SR-IOV VF ミニポート ドライバー](writing-sr-iov-vf-miniport-drivers.md)を参照してください。

 

 

 





