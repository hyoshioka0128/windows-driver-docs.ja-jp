---
title: チェンジャー デバイス制御要求の処理
description: チェンジャー デバイス制御要求の処理
ms.assetid: 3ee275c7-f2e4-47db-bd4b-db5c0c8ad399
keywords:
- チェンジャー ドライバー WDK のストレージ要求の処理
- 記憶域チェンジャー ドライバー WDK、要求の処理
- Ioctl WDK チェンジャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac5f163d74cb8a014f7b914186940a799db8d0d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538332"
---
# <a name="processing-changer-device-control-requests"></a>チェンジャー デバイス制御要求の処理


## <span id="ddk_processing_changer_device_control_requests_kg"></span><span id="DDK_PROCESSING_CHANGER_DEVICE_CONTROL_REQUESTS_KG"></span>


チェンジャー miniclass ドライバーでは、Ioctl を直接処理しません。 代わりに、チェンジャー クラス ドライバーによって処理される各 IOCTL に対応するルーチンがあります。

クラスのドライバーでは、要求を受信したときにパラメーターをチェックし、一定の前処理を実行します。 そのチェンジャー デバイス オブジェクトには IRP を受信するポインターを渡すこと、対応するチェンジャー miniclass ドライバー ルーチンを呼び出します。

チェンジャー miniclass ドライバーは、ユーザー デバイスに固有の確認が必要になるし、システム ポート ドライバーに送信する 1 つまたは複数のされる Srb のビルドを実行します。

成功すると、SRB、miniclass ドライバーのルーチンは、要求に関連する出力パラメーターに格納します。 SRB の成功または失敗、かどうか miniclass ドライバーのルーチンは通常、チェンジャー クラス ドライバーにポート ドライバーから受信した状態を返します。

 

 




