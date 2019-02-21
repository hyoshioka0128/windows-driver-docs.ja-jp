---
title: メモリ アクセス
description: メモリ アクセス
ms.assetid: a5265f2c-61b9-4f0f-8cff-05da26010c6a
keywords:
- デバッガー エンジン、メモリへのアクセス
- メモリへのアクセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3702792823bf2051abc3c6bbbb08fc1eea454696
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537389"
---
# <a name="memory-access"></a>メモリ アクセス


## <span id="ddk_memory_access_dbx"></span><span id="DDK_MEMORY_ACCESS_DBX"></span>


直接読み取りし、ターゲットのメイン メモリ、レジスタ、およびその他のデータ領域に書き込みするデバッガー エンジンです。

ユーザー モードのデバッグで、仮想メモリとレジスタのみにアクセスできます。物理メモリおよびその他のデータ領域にアクセスできません。

デバッガー エンジン API は、ターゲット上のメモリの場所を参照するときに必ず 64 ビットのアドレスを使用します。

ターゲットは、32 ビットのアドレスを使用している場合、ネイティブの 32 ビット アドレスが自動的に 64 ビットのアドレスにエンジンによって符号拡張します。 エンジンは、ターゲットと通信するときに自動的に 64 ビットのアドレスとネイティブの 32 ビット アドレスの間で変換されます。

このセクションの内容:

[仮想および物理メモリ](virtual-and-physical-memory.md)

[レジスタ](registers.md)

[その他のデータ領域](other-data-spaces.md)

 

 





