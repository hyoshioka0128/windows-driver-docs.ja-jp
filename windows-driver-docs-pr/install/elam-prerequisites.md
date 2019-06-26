---
title: ELAM の前提条件
description: 早期起動マルウェア対策ドライバーでは、WHQL で署名するのには、次のプログラム要件に従う必要があり、Windows によって読み込まれます。
ms.assetid: 48759EB3-F8F9-4881-BD30-6D1252F08DFE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e5625c7c261ec1bd1001a564ce116be97177059
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374998"
---
# <a name="elam-prerequisites"></a>ELAM の前提条件


早期起動マルウェア対策ドライバーがによって署名するのには、次のプログラム要件に従う必要があります**WHQL** Windows によって読み込まれるとします。

## <a name="antimalware-vendor-participation-requirements"></a>マルウェア対策ベンダーへの参加の要件


Microsoft では、起動時マルウェア対策ベンダーがいずれかのメンバーである必要があります、  **[Microsoft Virus Initiative (MVI)](https://docs.microsoft.com/windows/security/threat-protection/intelligence/virus-initiative-criteria)** します。 このメンバーシップにより、ベンダーが正の業界定評のあるアクティブなマルウェア対策コミュニティの参加者であるようになります。 MVI プログラムのメンバーではないし ELAM を使用する必要があると思われる場合にお問い合わせください **[ mvi@microsoft.com ](mailto:mvi@microsoft.com)** の追加情報。


## <a name="windows-hardware-quality-lab-whql-submission"></a>Windows Hardware Quality Lab (WHQL) の送信

-   記載されているように、ドライバーの検証を送信[ELAM ドライバーの送信](elam-driver-submission.md)
-   **WHQL**プロセスは事前起動のドライバーを提出する仕入先が許可されていることを確認します。  ない場合、MVI メンバー、または事前承認済みメンバーを使用して、お客様の提出は失敗します。
