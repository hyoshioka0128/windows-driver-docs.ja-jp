---
title: スマート カード設計ガイド
description: スマート カード設計ガイド
ms.assetid: 721A1530-B7B4-4373-9006-356A0A601349
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 714800ce1d24b0394c98210eeb817752ef54d23e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578821"
---
# <a name="smart-card-design-guide"></a>スマート カード設計ガイド


DDI スマート カードには、NFC コンタクトレス スマート カード上での低レベルのスマート カードの操作を実行するデバイス ドライバーの NFC 呼び出し元ができるようにします。 これは、カード到着/出発通知、スマート カード ATR、UID および履歴のバイトの情報などのメタデータを読み取るだけでなく Apdu を使用して特定の NFC カードに対する読み取り/書き込み操作の実行でリッスンしているが含まれます。 ISO14443 4 では非準拠のカード (ストレージ カードと呼ばれます) の Apdu のメモリ カードでサポートされる低レベルのプリミティブ コマンドへの変換は 4.3.7 セクションに記載されています。 Ioctl がスマート カード デバイスのドライバー インターフェイスを構成して、ファイルを使用して、それらのすべて\_ANY\_アクセスとメソッド\_バッファーに格納されました。 スマート カード DDI 以下は、スマート カード ドライバーを Windows で指定された Ioctl の最小サブセット\[1\]へのアクセスの NFC コンタクトレス スマート カードをサポートするためにします。

``` syntax
GUID_DEVINTERFACE_SMARTCARD_READER
“{50DD5230-BA8A-11D1-BF5D-0000F805F530}”
```

## <a name="unsupported-ioctls"></a>サポートされていない Ioctl


ドライバーがサポートされていないエラー コードを返す可能性がありますようになっているコンタクトレス スマート カードの操作で適用できないために、NFC のスマート カードの操作を次の Ioctl はサポートされていません。

-   IOCTL\_スマート カード\_取り出し
-   IOCTL\_スマート カード\_取得\_最後\_エラー
-   IOCTL\_スマート カード\_飲み込む

## <a name="smart-card-attributes"></a>スマート カードの属性
Windows スマート カード DDI には、Get と Set の属性の IOCTL 要求が含まれています。 NFC コンタクトレス リーダーをサポートする最小要件を満たすためにのみサポートされています、GET_ATTRIBUTE リーダーと ICC の状態の最小セット。 詳細については、[でサポートされるスマート カード属性](smart-card-attributes.md)を参照してください。

## <a name="in-this-section"></a>このセクションの内容


-   [機能のフロー](functional-flow.md)
-   [シーケンスの例](example-sequence.md)
-   [ストレージ カードの要件](storage-card-requirements.md)
-   [スマート カードのサポートされている属性](smart-card-attributes.md)
-   [PC/SC インターフェイス](pc-sc-interface.md)
 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[スマート カード DDI とコマンドのリファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905601)  

