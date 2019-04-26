---
title: Direct3D コンテキスト管理
description: Direct3D コンテキスト管理
ms.assetid: 143f5150-9ac4-43f7-985f-0baa32871af2
keywords:
- WDK Direct3D のコンテキスト
- Direct3D WDK Windows 2000 の表示、コンテキストの管理
- コンテキスト管理に関するコンテキスト WDK Direct3D、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c8e07b466c989b1dbcc4ef966b0be70b6532f1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342400"
---
# <a name="direct3d-context-management"></a>Direct3D コンテキスト管理


## <span id="ddk_direct3d_context_management_gg"></span><span id="DDK_DIRECT3D_CONTEXT_MANAGEMENT_GG"></span>


コンテキストは、アプリケーションで作成されたマイクロソフトの Direct3D ハードウェア アブストラクション レイヤー (HAL) デバイス; の状態情報をカプセル化します。つまり、コンテキストでは、ドライバーに描画する方法について説明します。 状態には、画面に表示される、画面の深度、網掛けは、およびテクスチャ情報などの情報が含まれています。

Direct3D ドライバーが作成して、独自のレンダリング コンテキストの管理を担当します。

 

 





