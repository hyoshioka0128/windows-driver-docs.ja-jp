---
title: '[UMDF Settings (Test Use Only)](UMDF 設定 (テスト使用のみ)) タブ'
description: このトピックでは、WDF Verifier の UMDF 設定 (テスト使用のみ) ページについて説明します。
ms.assetid: cce75c2e-fc93-4c17-9560-aef55451528b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acf49611495268e7c09928fe521b4c05b5c3378b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574211"
---
# <a name="umdf-settings-test-use-only-tab"></a>[UMDF Settings (Test Use Only)]\(UMDF 設定 (テスト使用のみ)\) タブ


このトピックについて詳しく説明 WDF Verifier の**UMDF 設定 (テスト使用のみ)** ページ。 このページで、1 つまたは複数のユーザー モード ドライバー フレームワーク (UMDF) ドライバーとシステム全体をテストするのに役立つ設定を変更できます。

テスト目的でこれらの設定を使用します。 完了したら、[テスト] をクリックして、**既定値に戻す**ボタンをクリックします。 それ以外の場合、コンピューターは、大幅なパフォーマンスの低下を示すことがあります。

![umdf 設定 (テスト使用のみ) タブのスクリーン ショット](images/wdfverifier-tab4.png)

既定で、 [UMDF インフライト レコーダー (IFR)](https://msdn.microsoft.com/library/windows/hardware/ff545531)システム クラッシュが発生した場合、ログを維持できますされるように、非ページ メモリに格納されます。 まれに、ただし、必要もあります非ページ メモリの領域を解放します。 たとえば、ストレス テストを複数の UMDF ドライバーとシステムはおそらく[デバイス プール](https://msdn.microsoft.com/library/windows/hardware/hh463993)オフ、および非ページ メモリがあります。 使用可能な非ページ メモリの少ない増加を取得するを選択すると、**使用ページ プール**ボックス。

また、場合によって分析などのツール Driver Verifier で十分な CPU の高いテスト ドライバー何の役にも UMDF の既定のタイムアウトがトリガーされるシステム パフォーマンスが低下することができますが正しくありません。 この場合、タイムアウト値を増やすことは、この種類の偶発的なタイムアウトを減らすことができます。

**警告**  
キャッチまたは UMDF ドライバーの障害を診断するために必要な場合にのみを使用する必要がありますの可能性を軽減することが実際にこれらのオプションを使用します。 システム全体をテストするために使用する方がいます。

 

 

 





