---
title: ELAM の前提条件
description: 早期起動マルウェア対策ドライバーでは、WHQL で署名するのには、次のプログラム要件に従う必要があり、Windows によって読み込まれます。
ms.assetid: 48759EB3-F8F9-4881-BD30-6D1252F08DFE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21799b9b7a3bb988d1cb2b128e504d0bceab3bd4
ms.sourcegitcommit: c340d6058fa3ea6407d0041de80482b88f623a90
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "59534162"
---
# <a name="elam-prerequisites"></a>ELAM の前提条件


早期起動マルウェア対策ドライバーがによって署名するのには、次のプログラム要件に従う必要があります**WHQL** Windows によって読み込まれるとします。

## <a name="antimalware-vendor-participation-requirements"></a>マルウェア対策ベンダーへの参加の要件


Microsoft では、起動時マルウェア対策ベンダーがいずれかのメンバーである必要があります、  **[Microsoft Virus Initiative (MVI)](https://www.microsoft.com/wdsi/alliances/virus-initiative)** します。 このメンバーシップにより、ベンダーが正の業界定評のあるアクティブなマルウェア対策コミュニティの参加者であるようになります。 MVI プログラムのメンバーではないし ELAM を使用する必要があると思われる場合にお問い合わせください**[ mvi@microsoft.com ](mailto:mvi@microsoft.com)** の追加情報。


## <a name="windows-hardware-quality-lab-whql-submission"></a>Windows Hardware Quality Lab (WHQL) の送信

-   記載されているように、ドライバーの検証を送信[ELAM ドライバーの送信](elam-driver-submission.md)
-   **WHQL**プロセスは事前起動のドライバーを提出する仕入先が許可されていることを確認します。  ない場合、MVI メンバー、または事前承認済みメンバーを使用して、お客様の提出は失敗します。
