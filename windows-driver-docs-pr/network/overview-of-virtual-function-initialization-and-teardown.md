---
title: 仮想関数の初期化と切断の概要
description: 仮想関数の初期化と切断の概要
ms.assetid: 2684A93A-40C2-49DA-925D-2BAACA9F8CD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e820d0fc55766f0bf410c49d9e858dc9f7555690
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372891"
---
# <a name="overview-of-virtual-function-initialization-and-teardown"></a>仮想関数の初期化と切断の概要


このセクションでは、PCI Express (PCIe) 仮想機能 (Vf) の初期化と破棄の順序の概要を示します。 VFs は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターによって提供されます。

ここでは、次のトピックについて説明します。

[仮想関数の初期化シーケンス](virtual-function-initialization-sequence.md)

[仮想関数の破棄順序](virtual-function-teardown-sequence.md)

SR-IOV 対応ネットワーク アダプターの VFs の詳細については、次を参照してください。 [SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)します。

**注**  だけで、PF ミニポート ドライバーは Vf などのネットワーク アダプターのハードウェア リソースを構成できます。 VF のミニポート ドライバーでは、SR-IOV 対応のアダプターのハードウェア リソースのほとんどを直接アクセスできません。 詳細については、次を参照してください。[書き込み SR-IOV VF ミニポート ドライバー](writing-sr-iov-vf-miniport-drivers.md)します。

 

 

 





