---
title: 保護レベルの処理
description: 保護レベルの処理
ms.assetid: d8237a48-9e1c-4b9e-8f55-70820ff08460
keywords:
- WDK COPP、保護レベルの保護をコピーします。
- ビデオのコピー防止 WDK COPP、保護レベル
- COPP WDK DirectX va なので、保護レベル
- ビデオの WDK COPP、保護レベルの保護
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 565b13026d18917bc1347f390de230f5a23bc724
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560937"
---
# <a name="handling-protection-levels"></a>保護レベルの処理


## <span id="ddk_handling_protection_levels_gg"></span><span id="DDK_HANDLING_PROTECTION_LEVELS_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

各出力には、保護をサポートするグラフィックス アダプターのコネクタが、ビデオのミニポート ドライバーは各種の保護と保護レベルごとにグローバル参照カウントを維持する必要があります。 既定のグローバル参照カウンターは 0 に初期化されていることに注意してください。

ビデオ セッションについては、DirectX VA COPP デバイスが作成されると、COPP デバイスは、各保護レベルの保護の種類ごとにローカルな参照カウントを含める必要があります。 ドライバーは、各保護の種類を値 1 に、各保護の種類、値 0 の残りの保護レベルのカウンターの既定の保護レベルのカウンターを設定する必要があります。

ビデオのセッションでは、特定の保護の種類の新しい保護レベルを設定、ドライバーは現在の保護レベルの参照カウントをデクリメントする必要があり、新しい保護レベルの参照カウントをインクリメントする必要があります。 対応する変更は、グローバル参照レベルのカウンターにも行ってください。

任意のグローバル レベルのカウンターが変更されるたびに、ドライバーは特定の出力のコネクタのすべてのカウンターを検査し、保護レベルが、値が 0 より大きい最高レベルのカウンターに対応するレベルに設定されていることを確認する必要があります。 詳細については、コード例を参照してください、 [ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)と[ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)ページを参照します。

グローバル参照カウンターが 0 より大きい、ビデオのミニポート ドライバーは出力コネクタにコンテンツ保護を適用する必要があります。 グローバル参照カウンターが 0 になるとすぐに、ビデオのミニポート ドライバーは、出力コネクタからコンテンツの保護を削除する必要があります。 ディスプレイ ドライバーがへの呼び出しを受信するたびにその[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)コールバック関数 (ビデオのミニポート ドライバーがさらへの呼び出しを受け取ると、その[ *COPPCloseVideoSession* ](https://msdn.microsoft.com/library/windows/hardware/ff539638)関数)、ビデオのミニポート ドライバーが COPP デバイスのローカル参照カウンターの現在のレベルでグローバル参照カウンターをデクリメントする必要があります。 ビデオのミニポート ドライバーがコネクタのグローバル参照カウンターが 0 になった場合、コンテンツ保護を認定出力コネクタから削除のみ必要があります。

**注**   、 *DdMoCompDestroy* COPP デバイスのローカル参照カウンターに設定されている (たとえば、ユーザー モード プロセスが異常終了) 場合、0 より大きい関数を呼び出すことがあります。

 

 

 





