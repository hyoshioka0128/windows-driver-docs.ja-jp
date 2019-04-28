---
title: 状態ブロックの記録とピュア デバイス
description: 状態ブロックの記録とピュア デバイス
ms.assetid: 9959d361-aa92-4209-8f81-deba96498941
keywords:
- DirectX 8.0 リリース ノート WDK Windows 2000 の表示では、純粋なデバイス、状態が処理をブロックします。
- 純粋なデバイス WDK DirectX 8.0 では、ブロックの処理を状態します。
- WDK DirectX 8.0 の処理状態のブロック
- WDK DirectX 8.0 では、純粋なデバイスの処理状態のブロック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c40c708ebf6429de76853bc5112dcbbb574b13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376012"
---
# <a name="state-block-recording-and-pure-devices"></a>状態ブロックの記録とピュア デバイス


## <span id="ddk_state_block_recording_and_pure_devices_gg"></span><span id="DDK_STATE_BLOCK_RECORDING_AND_PURE_DEVICES_GG"></span>


状態ブロックの処理は、純粋なデバイスのモードで動作しているデバイスによって異なります。 このモードでは、状態ブロック コントロール DP2 トークン (D3DDP2OP\_ステート セット) は新しい操作の種類のドライバーに送信されます (で、 **dwOperations**フィールド)。 この新しい操作の種類は D3DHAL\_STATESETCREATE します。

 

 





