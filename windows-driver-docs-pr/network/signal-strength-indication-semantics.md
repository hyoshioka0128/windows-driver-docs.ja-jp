---
title: 信号の強さを示す値のセマンティクス
description: 信号の強さを示す値のセマンティクス
ms.assetid: d28476f8-d567-4fe0-9cb9-4a78d8b0e05b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9bac44ddb9ed8d418ee1a8430cdaa351344c99a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536832"
---
# <a name="signal-strength-indication-semantics"></a>信号の強さを示す値のセマンティクス


次の図は、ミニポート ドライバーは、プロセスの信号強度の指示に従う必要があります、プロセスを示しています。 MB サービスは、信号の強度 reporting しきい値との間隔が現在のデバイス信号強度とどのくらいの時間、デバイスがアイドル状態に基づくを調整します。 これらのアクションは、通常、MB サービスによって提供される電源管理機能の一部として実行します。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![ミニポート ドライバーがプロセスの信号強度の指示に従う必要のあるプロセスを示す図](images/wwansignalstrength.png)

信号強度のインジケーターを更新するには、次の手順を使用します。

1.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931) MB サービスにします。

2.  MB サービスが送信[OID\_WWAN\_信号\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569836)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認応答 (NDIS\_状態\_INDICATION\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信します。

3.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

4.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931) MB サービスにします。

5.  MB サービスが送信[OID\_WWAN\_信号\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569836)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認応答 (NDIS\_状態\_INDICATION\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信します。

6.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

7.  MB サービスが送信[OID\_WWAN\_信号\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569836)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認応答 (NDIS\_状態\_INDICATION\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信します。

8.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

9.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931) MB サービスにします。

 

 





