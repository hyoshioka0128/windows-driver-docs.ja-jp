---
title: シーケンスの例
ms.assetid: 2B15570A-A220-4BF7-B595-D9CF66E02673
keywords:
- スマートカードリソースマネージャーにおける、スタートアップ接続と切断を含む Ioctl のシーケンスの例
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: 起動時、接続、切断など、スマートカードリソースマネージャーの Ioctl のシーケンスの例を示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff748d7c696c5c0abf46e539a65c92aca542d89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843413"
---
# <a name="example-sequence"></a>シーケンスの例


次に、スマートカードリソースマネージャーにおける Ioctl のシーケンス例を示します。

## <a name="start-up-sequence"></a>スタートアップシーケンス


1.  DevObj または CfgMgr API とスマートカードアクセスデバイスインターフェイスの GUID を使用して、NFC デバイスドライバーの名前を検出し、それを CreateFile と共に使用してデバイスハンドルを開きます。

2.  スレッドプールを初期化します。

3.  閲覧者名を決定します。

    -   IOCTL\_スマートカード\_破棄\_ATTR\_VENDOR\_NAME、破棄\_ATTR\_VENDOR\_IFD\_TYPE、破棄\_ATTR\_デバイスの\_属性を取得し\_ユニット

4.  リーダーの特性を決定します。
    -   IOCTL\_スマートカード\_破棄\_ATTR\_特性の\_属性を取得します。

5.  カード状態モニターを起動します。
    -   スマートカードの到着を待機するために、IOCTL\_スマートカード\_が存在\_。

    -   スマートカードの出発を待機するために、IOCTL\_スマートカード\_は存在し\_いません。

破棄\_飲み込む、破棄\_電源状態がサポートされていないため、電源リセットは関係ありません。

## <a name="connect-sequence"></a>接続シーケンス


1.  ループの開始。

2.  スマートカードによる\_状態の取得\_IOCTL\_

    -   Case 破棄\_UNKNOWN と破棄\_存在しません。何も行いません。

    -   Case 破棄\_PRESENT、飲み込む card

    -   ケース破棄\_飲み込む、コールドリセット

    -   ケース破棄\_電源、ウォームリセット

    -   ケース破棄\_の譲渡、カード ATR の特定

    -   ケース破棄\_固有で、カードの ATR とプロトコルを決定します。

3.  スマートカードの IOCTL\_\_プロトコルの設定\_

## <a name="disconnect-sequence"></a>シーケンスの切断


1.  電源ダウンタイムアウトが開始されます。

2.  ループの開始。

3.  スマートカードによる\_状態の取得\_IOCTL\_

    -   大文字と小文字の区別\_具体的には、破棄\_譲渡、破棄\_電源、電源をオンに設定

    -   Case 破棄\_飲み込む、破棄\_PRESENT、nothing

    -   Case 破棄\_存在しない、破棄\_UNKNOWN、do nothing

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[スマートカード DDI とコマンドリファレンス](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85))  
