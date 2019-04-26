---
title: 物理アドレスによるメモリへのアクセス
description: 物理アドレスによるメモリへのアクセス
ms.assetid: 248871dc-dac0-413e-8971-2ee2c2fe5290
keywords:
- 物理アドレス、メモリへのアクセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21c56460649584f009fd49636646ea3620fa3380
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351887"
---
# <a name="accessing-memory-by-physical-address"></a>物理アドレスによるメモリへのアクセス


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


物理アドレスからの読み取り、使用、 [ **! db**](-db---dc---dd---dp---dq---du---dw.md)、 **! dc**、 **! dd**、 **! dp**、 **! du**、および **! dw**拡張コマンド。

物理アドレスに書き込むを使用して、 [ **! eb** ](-eb---ed.md)と **! ed**拡張コマンド。

[ **Fp (物理メモリの入力)** ](f--fp--fill-memory-.md)範囲がいっぱいになるまで繰り返しコマンドは、物理メモリの範囲にパターンを書き込みます。

WinDbg を使用して、カーネル モードの場合は、することができますも読み取りまたは書き込みを物理メモリから直接、[メモリ ウィンドウ](memory-window.md)します。

物理メモリのデータまたはデータの範囲を検索するには、使用、 [ **! 検索**](-search.md)拡張機能コマンド。

また、物理アドレスの詳細についてを参照してください[仮想のアドレスを物理アドレスを変換する](converting-virtual-addresses-to-physical-addresses.md)します。

 

 





