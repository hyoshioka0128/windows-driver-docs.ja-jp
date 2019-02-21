---
title: NFC クラスの拡張機能
description: このセクションでは、NFC クラス拡張 (CX) と、NFC クライアント ドライバー間のインターフェイスについて説明します。
ms.assetid: 64599C5E-7E72-4712-B733-24C078919B84
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
- CX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25ff8f74e80942dc8d8578e9921cf23e9b7995a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537862"
---
# <a name="nfc-class-extension-cx-design-guide"></a>NFC クラスの拡張機能 (CX) 設計ガイド


このセクションでは、NFC クラス拡張 (CX) と、NFC クライアント ドライバー間のインターフェイスについて説明します。 NFC CX ドライバーではすべての NFC デバイス ドライバー インターフェイスと標準の NFC プロトコルと形式に基づいて、 *NFC フォーラム NFC コント ローラー インターフェイス (NCI) の技術仕様*します。

NFC のクライアント ドライバーでは、トランスポート層の NFC コント ローラーの最適化された機能の非標準ベンダー定義拡張機能のサポートとやり取りを担当します。

すべての標準の NFC フォーラム タグ (T1T、T2T、T3T、ISO DEP) と P2P NFC クラスの拡張機能ドライバーを実装して、NCI のコア仕様に基づいて (LLCP および SNEP) のプロトコル、および RF 管理します。 クラスの拡張機能ドライバーでは、NFC コント ローラー、要素のセキュリティで保護されたリモート RF エンドポイントと対話するすべての Windows で定義されているデバイス ドライバー インターフェイスを実装します。

これらのトピックでは、アーキテクチャと Microsoft と対応するチップセット メーカーが付属している NFC クライアント ドライバーによって提供される NFC クラスの拡張機能ドライバーの間でのパブリック インターフェイスについて説明します。 NFC CX ドライバーは、さまざまな製造元は、NFC チップセットをサポートするために設計されていますされ差別化のための NFC クライアント ドライバーで NCI 非標準の機能を実装するために製造元できます。

## <a name="nfc-driver-ddi"></a>NFC ドライバー DDI
次に、Windows による NFC ドライバー DDI NFC CX ドライバーによって実装されています。

-   [フィールドの近接 DDI 近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)
-   [NFC 要素をセキュリティで保護された管理 DDI](https://msdn.microsoft.com/library/windows/hardware/dn905485)
-   [スマート カード DDI になっているコンタクトレス スマート カードのアクセス](https://msdn.microsoft.com/library/windows/hardware/dn905601)
-   [DDI の NFC 無線管理](https://msdn.microsoft.com/library/windows/hardware/dn905577)
-   DTA DDI NFC フォーラムの認定資格

## <a name="nfc-forum-specifications"></a>NFC フォーラムの仕様
次に、NFC CX ドライバーによって実装される NFC フォーラムの仕様を示します。  

-   NFC のコント ローラーのインターフェイス、NCI 1.0 仕様
-   NFC のデータ交換形式、NDEF
-   NFC フォーラムは、1 ~ 4 のタグを入力します。
-   論理リンク制御プロトコル、LLCP 1.1 仕様
-   単純な NDEF 交換プロトコル、SNEP 1.0 仕様
-   ISO/IEC 15693

## <a name="supported-nfc-smart-cards-and-tags"></a>NFC のスマート カードとタグのサポート
NFC のスマート カードと NFC CX ドライバーでサポートされているタグを次に示します。  

-   MIFARE クラシック ファミリ
-   MIFARE おり、超軽量のファミリ
-   MIFARE DESFire ファミリ
-   FeliCa ファミリ
-   ジュエル/Topaz ファミリ
-   汎用 ISO 15693 タグします。
-   Thinfilm NFC バーコード (Kovio)



## <a name="in-this-section"></a>このセクションの内容


-   [用語集](glossary.md)
-   [アーキテクチャ](architecture.md)
-   [NFC スタック アーキテクチャ](nfc-stack-architecture.md)
-   [ドライバーの読み込み順序](driver-load-order.md)
-   [クラスの拡張機能インターフェイス](nfc-class-extension-interface.md)
-   [クラスの拡張機能のステート マシン](nfc-class-extension-state-machine.md)
-   [機能拡張モデル](extensibility-model.md)
-   [構成機能](configurability.md)
-   [エラーの処理](error-handling.md)
-   [電源の状態](power-states.md)
-   [NFC クライアント ドライバーの電源管理の要件](nfc-client-driver-power-management-requirements.md)
-   [ログ記録](logging.md)
-   [永続化されたデータ](persisted-data.md)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_nfpdrivers/)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/)  
