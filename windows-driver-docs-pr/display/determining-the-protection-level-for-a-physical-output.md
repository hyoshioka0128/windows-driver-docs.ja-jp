---
title: 物理的な出力の保護レベルの決定
description: 物理的な出力の保護レベルの決定
ms.assetid: ea06903a-0ad5-43fd-b2d3-013584ae6f69
keywords:
- 保護レベルの物理的な出力を決定する、WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efc6ae4e16b771eb4bab21c3c490042a4ff63cec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348825"
---
# <a name="determining-the-protection-level-for-a-physical-output"></a>物理的な出力の保護レベルの決定


物理的なビデオ出力コネクタの保護レベルを決定するのに、次のセクションでアルゴリズムを使用する必要があります。 これらのアルゴリズムは、擬似コードで表現されます。

### <a name="span-idalgorithmforprotectionlevelspanspan-idalgorithmforprotectionlevelspanalgorithm-for-protection-level"></a><span id="algorithm_for_protection_level"></span><span id="ALGORITHM_FOR_PROTECTION_LEVEL"></span>保護レベルのアルゴリズム

物理的なビデオ出力コネクタの保護レベル値を決定するのに、次のアルゴリズムを使用する必要があります。

1.  **各**物理出力コネクタをサポートする保護タイプ (ACP では、CGMS A、HDCP、および DPCP) は、次の手順を実行します。
    1.  出力保護なしには、提案された保護レベルを設定します。 たとえば、ACP では、ドライバーをする必要があります保護レベルに設定 DXGKMDT\_OPM\_ACP\_オフは CGMS は、ドライバーは、保護レベルを設定 DXGKMDT\_OPM\_CGMSA\_オフになります。HDCP のドライバーは、DXGKMDT に保護レベルを設定する必要があります\_OPM\_HDCP\_ドライバーが DXGKMDT に保護レベルを設定する必要があります OFF; と DPCP は、\_OPM\_DPCP\_オフにします。
    2.  **各**物理出力コネクタに関連付けられている保護されている出力は次の手順を実行します。
        1.  現在の保護の種類の保護レベルを現在の保護された出力を取得します。
        2.  **場合**現在保護の種類は CGMS-A、削除、DXGKMDT\_OPM\_再配布\_コントロール\_フラグが設定されている場合に必須フラグ。
        3.  **場合を終了します。**
        4.  **場合**現在保護されている出力の保護レベルが提案された保護レベルより高い優先順位を持つ、現在保護されている出力の保護レベルに提案された保護レベルを設定します。
        5.  **場合を終了します。**

    3.  **終了**
    4.  提案された保護レベルを物理出力の保護レベルを設定します。

2.  **終了**

### <a name="span-idalgorithmforredistributioncontrolspanspan-idalgorithmforredistributioncontrolspanalgorithm-for-redistribution-control"></a><span id="algorithm_for_redistribution_control"></span><span id="ALGORITHM_FOR_REDISTRIBUTION_CONTROL"></span>コントロールの再配布するためのアルゴリズム

次のアルゴリズムを使用して、物理出力コネクタがコントロールの再配布を有効にする必要があるかどうかを判断する必要があります。

1.  **各**物理出力コネクタに関連付けられている保護されている出力は次の手順を実行します。
    1.  現在保護されている出力の再配布制御フラグが設定されているかの情報を取得します。
    2.  **場合**、DXGKMDT\_OPM\_再配布\_コントロール\_必須フラグが設定されて、次の手順に従います。
        1.  コントロールの再配布を有効にします。
        2.  アルゴリズムの実行を停止します。

    3.  **場合を終了します。**

2.  **終了**

 

 





