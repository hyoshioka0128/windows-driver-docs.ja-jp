---
title: PTP エラー コード
description: PTP エラー コード
ms.assetid: 4d7ad081-fc0b-4a9e-8f17-a0c98fa4fa50
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eca63726c0b5604ec167b8d3fc34a2c5c2d6d786
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379626"
---
# <a name="ptp-error-codes"></a>PTP エラー コード





Microsoft PTP WIA ミニドライバーは、エラーを検出すると、WIA に応答コードを渡します。 PTP カメラ 0x2001 (OK) 以外の応答を返す場合、WIA ミニドライバーは、HRESULT エラー コードとしてラップ応答コードを返します。 エラー コードの形式は、0x8004XXXX、XXXX が 4 つの 16 進数の応答コードを表します。 これは特定の PTP カメラを使用するように設計された WIA アプリケーションを非常に役立ちます。 エラー/状態情報は、エンドユーザーに報告する豊富な状態に保持されます。

 

 




