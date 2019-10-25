---
title: NFC クライアント ドライバーの電源の管理要件
ms.assetid: FBA0821B-859F-4A44-998E-E00162FBD265
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: コネクトスタンバイでの NFP デバイスの要件の達成に関する情報。 ・
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d31fa09026ad5444575987d22acfe5a15039ae6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831871"
---
# <a name="nfc-client-driver-power-management-requirements"></a>NFC クライアント ドライバーの電源の管理要件


NFC クライアントドライバーは、接続されたスタンバイプラットフォームでの NFP デバイスの要件を満たすために、次のように D0 および D3 の電源処理コールバックを実装する必要があります。

-   NFC クライアントドライバーは、ドライバーが D3&gt; D0 状態から復帰するときに、100ミリ秒未満で再開できることを確認する必要があります。 これは、画面の切り替え時に NFC 操作が直ちに行われるようにするためです。

-   また、D3 状態の場合、NFC クライアントドライバーは電力消費が 1 Mw 未満であることを確認する必要があります。 これは、画面をオフにしたときの電力消費が非常に少ないことを確認するためのものです。

これらの目標を達成するために、NFC クライアントドライバーには次のことをお勧めします。

-   これらの要件を満たすことができる NFC コントローラーは、電源が入っていないか、またはハードな電源がオフになっているため、NFC クライアントドライバーで、D0-&gt; D3 の間にチップセットを再初期化し、次に D3 から&gt; D0 への移行を行うことをお勧めします。

-   非揮発性 (RAM ベース) のメモリが不足しているために修正プログラムをダウンロードする必要がある NFC コントローラーの場合、NFC クライアントドライバーでは、D0&gt; D3 および D3&gt; D0 の遷移時にそれぞれ、スタンバイモードを有効または無効にすることをお勧めします。 完全な初期化が実行されます (HostActionStart)。&gt; D3Final から開始すると、deinitialization (Hostactionstart) が D0-&gt; D3Final から移動するときに実行されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
