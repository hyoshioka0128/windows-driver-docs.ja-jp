---
title: NFC クラス拡張
description: このセクションでは、NFC クラス拡張 (CX) と NFC クライアントドライバー間のインターフェイスについて説明します。
ms.assetid: 64599C5E-7E72-4712-B733-24C078919B84
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
- シリーズ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94a1b1b94f78b36e0e7dd6249111bc45e8989aca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842743"
---
# <a name="nfc-class-extension-cx-design-guide"></a>NFC クラスの拡張 (CX) 設計ガイド


このセクションでは、NFC クラス拡張 (CX) と NFC クライアントドライバー間のインターフェイスについて説明します。 Nfc CX ドライバーは、nfc*フォーラム Nfc Controller Interface (NCI) の技術仕様*に基づいて、すべての nfc デバイスドライバーインターフェイスと標準 nfc プロトコルと形式を実装します。

NFC クライアントドライバーは、トランスポート層のインターフェイスに加えて、NFC コントローラーの最適化された機能を提供する、標準以外のベンダー定義の拡張機能のサポートを担当します。

NFC クラス拡張ドライバーは、すべての標準 NFC フォーラムタグ (T1T、T2T、T3T、ISO-DEP) と P2P (LLCP and SNEP) プロトコル、および NCI Core 仕様に基づく RF 管理を実装します。 クラス拡張ドライバーは、NFC コントローラー、セキュリティで保護された要素、およびリモートの RF エンドポイントと対話するために、Windows で定義されたすべてのデバイスドライバーインターフェイスを実装します。

これらのトピックでは、Microsoft が提供する NFC クラス拡張ドライバーと、対応するチップセット製造元によって提供される NFC クライアントドライバーとの間のアーキテクチャとパブリックインターフェイスについて説明します。 NFC CX ドライバーは、さまざまな製造元からの NFC チップセットをサポートするように設計されています。また、製造元は、NCI のない標準機能を NFC クライアントドライバーに実装して区別することができます。

## <a name="nfc-driver-ddi"></a>NFC ドライバー DDI
NFC CX ドライバーによって実装される Windows で定義された NFC ドライバー DDI を次に示します。

-   [近距離無線近接 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [NFC Secure 要素管理 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [Contactless スマートカードアクセス用のスマートカード DDI](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85))
-   [NFC 無線管理 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   NFC フォーラム認定のための DTA DDI

## <a name="nfc-forum-specifications"></a>NFC フォーラム仕様
NFC CX ドライバーによって実装される NFC フォーラム仕様は次のとおりです。  

-   NFC コントローラーインターフェイス、NCI 1.0 仕様
-   NFC データ交換形式、NDEF
-   NFC フォーラムタイプ1-4 タグ
-   論理リンク制御プロトコル、LLCP 1.1 仕様
-   Simple NDEF Exchange Protocol、SNEP 1.0 仕様
-   ISO/IEC 15693

## <a name="supported-nfc-smart-cards-and-tags"></a>サポートされている NFC スマートカードとタグ
NFC CX ドライバーでサポートされている NFC スマートカードとタグを次に示します。  

-   MIFARE クラシックファミリ
-   MIFARE Ultralight ファミリ
-   MIFARE DESFire ファミリ
-   FeliCa ファミリ
-   フォントファミリ
-   汎用 ISO 15693 タグ
-   Thinfilm NFC バーコード (Kovio)



## <a name="in-this-section"></a>このセクションの内容


-   [用語集](glossary.md)
-   [アーキテクチャ](architecture.md)
-   [NFC スタックのアーキテクチャ](nfc-stack-architecture.md)
-   [ドライバーの読み込み順序](driver-load-order.md)
-   [クラス拡張インターフェイス](nfc-class-extension-interface.md)
-   [クラス拡張のステートマシン](nfc-class-extension-state-machine.md)
-   [機能拡張モデル](extensibility-model.md)
-   [かつ](configurability.md)
-   [エラーの処理](error-handling.md)
-   [パワー状態](power-states.md)
-   [NFC クライアントドライバーの電源管理要件](nfc-client-driver-power-management-requirements.md)
-   [ログ](logging.md)
-   [永続化されたデータ](persisted-data.md)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_nfpdrivers/)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/)  
