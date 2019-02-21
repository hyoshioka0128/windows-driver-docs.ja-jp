---
title: HFP デバイスの削除
description: HFP デバイス削除のトピックでは、(リーフ) から Bluetooth ハンズフリー プロファイル (HFP) デバイスが削除されるときの動作について説明します、オーディオ システム。
ms.assetid: 99B6C09E-2467-4124-9F9A-5116586BB38C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b13e5dcb722b69a131ebbca0d4439dffef02a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549572"
---
# <a name="hfp-device-removal"></a>HFP デバイスの削除


HFP デバイス削除のトピックでは、(リーフ) から Bluetooth ハンズフリー プロファイル (HFP) デバイスが削除されるときの動作について説明します、オーディオ システム。

ペアになっている HFP デバイス、オーディオ ドライバーの登録済みデバイスのインターフェイスを削除するには。

1. キャンセル保留中の IOCTL\_BTHHFP\_スピーカー\_取得\_ボリューム\_状態\_更新 Ioctl します。

2. キャンセル保留中の IOCTL\_BTHHFP\_ストリーム\_取得\_状態\_更新 Ioctl します。

3. キャンセル保留中の IOCTL\_BTHHFP\_デバイス\_取得\_接続\_状態\_更新 Ioctl します。

4. 解除 HFP FileObject (これも、デバイス オブジェクトを逆参照) を参照します。

5. 削除されたインターフェイスに関連付けられた HFP デバイスを表すフィルター ファクトリを削除する KsDeleteFilterFactory を呼び出します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[操作の理論を概説します。](theory-of-operation.md)  



