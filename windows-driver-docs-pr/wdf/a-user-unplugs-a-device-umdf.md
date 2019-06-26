---
title: ユーザーがデバイスを取り外す
description: ユーザーがデバイスを取り外す
ms.assetid: d0c8fd6d-b356-4048-aa97-ebe331d23361
keywords:
- 電源管理のシナリオ、デバイスのプラグを抜くの WDK UMDF
- デバイスのシナリオ WDK UMDF を取り外す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36a1766d8a27a380ee95f0f01656324254c57a89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385329"
---
# <a name="a-user-unplugs-a-device"></a>ユーザーがデバイスを取り外す


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

システムの実行中に、ユーザー、デバイスを削除できます、次のいずれかの 2 つの方法: によって*正しく削除*、つまり、ユーザーでは、システムが通知 (たとえば、取り外しまたは取り出しを使用して削除される直前に、デバイスがあります。ハードウェアのプログラムの場合)。または*突然の取り外し*ユーザーがシステムに通知することがなく、デバイスをコールバックすることを意味します。 バスは、突然の取り外し (USB など) をサポートする場合、デバイスのドライバーは、デバイスの急激な消滅を処理できる必要があります。

<a href="" id="orderly-removal-------"></a>**所定の削除**   
ユーザーは、デバイス マネージャーを使用して、デバイスを無効にすると、システムの取り外しますプログラムを使用して削除を要求するか、イジェクト ボタンを押して移動可能なリムーバブル デバイスの。 フレームワークによりを削除または無効にすると、デバイス ドライバーが提供されている場合を除き、 [ **IPnpCallback::OnQueryRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-onqueryremove)コールバック関数、およびコールバック関数を削除が拒否しました。

次の図は、電源ダウンと削除の UMDF コールバックのシーケンスを示します。 シーケンスは、図の上部にある作業の電源の状態 (D0) にあるデバイスで開始します。

![umdf ドライバーのデバイスで整然と電源の削除の順序](images/umdf-powerdown-sequence.png)

<a href="" id="surprise-removal-------"></a>**突然の取り外し**   
このシナリオで、ユーザーから切り離し、デバイスが予期せずします。 UMDF を呼び出し、突然削除シーケンスで、 [ **IPnpCallback::OnSurpriseRemoval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-onsurpriseremoval)にデバイスが予期せず削除されたことをドライバーに通知するコールバック。 このコールバックは、特定の順序で削除シーケンス内の他のコールバックで発生することは保証されません。

一般に、ドライバーでは、削除のパス内のハードウェアへのアクセスを避ける必要があります。 ハードウェアへのアクセスには無期限に待機している場合、reflector がタイムアウトしました。 次の図は、UMDF ドライバーの突然削除順序を示します。

![umdf ドライバーの突然の取り外しシーケンス](images/umdf-surprise-removal-sequence.png)

 

 





