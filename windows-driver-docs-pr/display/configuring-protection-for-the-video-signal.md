---
title: ビデオ信号の保護を構成します。
description: ビデオ信号の保護を構成します。
ms.assetid: 557fc95b-1cf5-4b6d-b256-fe2db29ec0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 515087445e362a99f87c3e953d060d5a5ad1f53c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529381"
---
# <a name="configuring-protection-for-the-video-signal"></a>ビデオ信号の保護を構成します。


OPM 構成では、保護された出力に関連付けられている物理コネクタを経由するビデオ信号の保護を構成できます。 シグナル保護まで、ディスプレイのミニポート ドライバーの設定に[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)関数へのポインターを受け取る、 [ **DXGKMDT\_OPM\_構成\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560849)構造体、 **guidSetting**メンバー設定、DXGKMDT\_OPM\_セット\_ACP\_AND\_CGMSA\_シグナリングの GUID と**abParameters**メンバーへのポインターに設定、 [ **DXGKMDT\_OPM\_設定\_ACP\_AND\_CGMSA\_シグナリング\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560913)信号を保護する方法を指定する構造体。

 

 





