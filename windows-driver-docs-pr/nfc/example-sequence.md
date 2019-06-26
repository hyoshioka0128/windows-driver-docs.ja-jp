---
title: シーケンスの例
ms.assetid: 2B15570A-A220-4BF7-B595-D9CF66E02673
keywords:
- スタートアップの接続と切断を含む、スマート カード リソース マネージャーでの Ioctl のシーケンスの例
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: スマート カード リソース マネージャーで、起動、接続、切断などの Ioctl のシーケンスの例を示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d85138dfb1fe9ee298d72c85d8788709ac55888
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370524"
---
# <a name="example-sequence"></a>シーケンスの例


スマート カード リソース マネージャーでの ioctl 例シーケンスを次に示します。

## <a name="start-up-sequence"></a>起動シーケンス


1.  スマート カードのアクセスのデバイス インターフェイスの GUID を DevObj または CfgMgr API を使用して、NFC デバイス ドライバーの名前を検出し、CreateFile でデバイス ハンドルを開くために使用します。

2.  スレッド プールを初期化します。

3.  リーダーの名前を決定します。

    -   IOCTL\_スマート カード\_取得\_s カード属性\_ATTR\_ベンダー\_名、s カード\_ATTR\_ベンダー\_IFD\_型、および s カード\_ATTR\_デバイス\_単位

4.  リーダーの特性を決定します。
    -   IOCTL\_スマート カード\_取得\_s カード属性\_ATTR\_特性

5.  カードの状態のモニターを起動します。
    -   IOCTL\_スマート カード\_IS\_スマート カードの到着を待機する – 存在します。

    -   IOCTL\_スマート カード\_IS\_ABSENT – スマート カードからを待機します。

電源リセットは、s カードはサポートされていませんので、関連する\_SWALLOWED、s カード\_電源の状態。

## <a name="connect-sequence"></a>シーケンスを接続します。


1.  ループの開始。

2.  IOCTL\_スマート カード\_取得\_状態

    -   大文字の s カード\_不明および s カード\_ABSENT、何もしません。

    -   大文字の s カード\_現在のところ、理解しカード

    -   大文字の s カード\_受け入れられる、コールド リセット

    -   大文字の s カード\_リセットを利用した、ウォーム

    -   大文字の s カード\_ネゴシエーション可、カードの ATR を確認

    -   大文字 s カード\_特定、カード ATR とプロトコルの確認

3.  IOCTL\_スマート カード\_設定\_プロトコル

## <a name="disconnect-sequence"></a>シーケンスを切断します。


1.  電源のタイムアウトが開始されます。

2.  ループの開始。

3.  IOCTL\_スマート カード\_取得\_状態

    -   大文字の s カード\_特定、s カード\_ネゴシエーション可、s カード\_設定の電源を

    -   大文字の s カード\_SWALLOWED、s カード\_存在する場合は、何もしません。

    -   大文字の s カード\_不在であれば、s カード\_不明は、何もしません。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[スマート カード DDI とコマンドのリファレンス](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85))  
