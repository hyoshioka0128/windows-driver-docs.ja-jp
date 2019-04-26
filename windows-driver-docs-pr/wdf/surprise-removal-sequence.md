---
title: 突然の取り外しのシーケンス
description: 突然の取り外しのシーケンス
ms.assetid: 5A89BEDA-BAC3-476F-99B3-4E6E6DDDE5F5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c90800119f063f7bf039e05346ff13c0b13a661
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350682"
---
# <a name="surprise-removal-sequence"></a>突然の取り外しのシーケンス


ユーザーは、デバイス マネージャーまたはハードウェアの安全なユーティリティを使用せず切断するだけで、警告なしのデバイスを削除した場合、デバイスが「驚くことで削除されます」と見なされます この場合、フレームワークは若干異なる削除順序に従います。 別のドライバーを呼び出す場合も、突然削除シーケンスを従うこと[ **IoInvalidateDeviceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549361)デバイスで、でも、デバイスが物理的に存在する場合。 突然削除順番では、フレームワーク、 [ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)削除シーケンスで、他のコールバックを呼び出す前にコールバックします。 シーケンスが完了したら、フレームワークは、デバイス オブジェクトを破棄します。 すべてのリムーバブル デバイスのドライバーの障害、ハードウェアの削除によって引き起こされるエラー特にスタートアップとシャット ダウンの両方のパス内のコールバックを処理できる必要がありますを確認します。 ハードウェアにアクセスしようは、無期限に待機する必要がありますが、タイムアウトやウォッチドッグ タイマーにする必要があります。

次の図では、突然の削除に関連するコールバックを示しています。

![シーケンスの突然の取り外し](images/surprise-removal.png)

削除したとき、デバイスは稼働状態にありませんが場合、フレームワーク、 [ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)イベント コールバックの直後に[ *EvtDeviceSurpriseRemoval*](https://msdn.microsoft.com/library/windows/hardware/ff540913)します。 デバイスの動作状態から終了時に実行された既に、介在する手順が省略されます。

 

 





