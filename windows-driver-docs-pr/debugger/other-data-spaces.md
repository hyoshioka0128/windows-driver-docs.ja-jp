---
title: その他のデータ領域
description: その他のデータ領域
ms.assetid: f676a478-c02a-4400-8173-a1b3103c6c1b
keywords:
- デバッガーのエンジンの API、メモリ、データ領域
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 590e163be1ef518f007585244c1952cbf523c9db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527520"
---
# <a name="other-data-spaces"></a>その他のデータ領域


## <span id="ddk_other_data_spaces_dbx"></span><span id="DDK_OTHER_DATA_SPACES_DBX"></span>


カーネル モードのデバッグ、さまざまなメイン メモリやレジスタに加えてデータ領域にデータを読み書きすることです。 次のデータ領域にアクセスできます。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>システム バス  
メソッド[ **ReadBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff553519)と[ **WriteBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff561371)システム バス データを読み書きします。

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>コントロールの領域のメモリ  
メソッド[ **ReadControl** ](https://msdn.microsoft.com/library/windows/hardware/ff553524)と[ **WriteControl** ](https://msdn.microsoft.com/library/windows/hardware/ff561374)コントロール領域のメモリを読み書きします。

<span id="i_o_memory."></span><span id="I_O_MEMORY."></span>I/O メモリ。  
メソッド[ **ReadIo** ](https://msdn.microsoft.com/library/windows/hardware/ff553573)と[ **WriteIo** ](https://msdn.microsoft.com/library/windows/hardware/ff561402)読み取りおよびシステムを書き込み、および I/O メモリ バスします。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>モデル専用レジスタ (MSR)  
メソッド[ **ReadMsr** ](https://msdn.microsoft.com/library/windows/hardware/ff554292)と[ **WriteMsr** ](https://msdn.microsoft.com/library/windows/hardware/ff561424) 、制御レジスタを有効にして、機能を無効にするには、MSRs の読み書きとデバッグ、CPU の特定のモデルをサポートします。

### <a name="span-idhandlesspanspan-idhandlesspan-handles"></a><span id="handles"></span><span id="HANDLES"></span> ハンドル

ユーザー モードのデバッグは、ターゲット プロセスによって所有されているシステム ハンドルを使用してシステム オブジェクトに関する情報を取得できます。 メソッド[ **ReadHandleData** ](https://msdn.microsoft.com/library/windows/hardware/ff553542)この情報を読み取ることができます。

スレッドとプロセスのシステム オブジェクトに対してシステム ハンドルを使用して取得できます、 [ **GetCurrentThreadHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff545904)と[ **GetCurrentProcessHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff545816)メソッド。 これらのハンドルにも用意されています、 [ **IDebugEventCallbacks::CreateThread** ](https://msdn.microsoft.com/library/windows/hardware/ff550713)と[ **IDebugEventCallbacks::CreateProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff550697)複数のスレッドが作成し、作成プロセスのデバッグ イベントが発生したときのコールバック メソッド。

**注**  カーネル モードでプロセスとスレッドのハンドルには、人為的なハンドル。 処理システムではありません。

 

 

 





