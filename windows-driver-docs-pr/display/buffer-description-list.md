---
title: バッファーの説明の一覧
description: バッファーの説明の一覧
ms.assetid: 7d820491-2df2-4036-8f3d-e6bcff4cd1f6
keywords:
- ビデオのデコード WDK DirectX va なので、バッファーの説明の一覧
- ビデオの WDK DirectX va なので、バッファーの説明の一覧のデコード
- WDK の DirectX va なので、バッファーの説明の一覧をデコードする画像
- WDK DirectX VA をバッファー処理します。
- 説明の一覧の WDK DirectX VA をバッファーします。
- DXVA_BufferDescription
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aaea7ebea615fceac2d37bfc4af5a7fb2bc79ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528147"
---
# <a name="buffer-description-list"></a>バッファーの説明の一覧


## <span id="ddk_buffer_description_list_gg"></span><span id="DDK_BUFFER_DESCRIPTION_LIST_GG"></span>


DirectX VA は、主に、ホスト デコーダーから、ハードウェア アクセラレータにデータのバッファーを渡すことによって動作します。 アクセラレータにホストからのバッファー セットが渡されるバッファーを記述するバッファーの説明の一覧が送信されます。 バッファーの説明の一覧は、配列の[ **DXVA\_BufferDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff563122)構造体。 バッファーの説明の一覧には、1 つの DXVA が含まれています。\_送信されるバッファーのセット内の各バッファーの BufferDescription 構造体。 バッファーの説明の一覧から 1 つまたは複数の DXVA 始まります\_BufferDescription 構造体が送信されるバッファーの最初の型。 これは、後に 1 つまたは複数の DXVA\_BufferDescription 構造体が送信されるバッファーの次の種類。

値、 **dwTypeIndex**のメンバー、 [ **DXVA\_BufferDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff563122)構造体は、ホストから渡されるバッファーの種類を指定します、アクセラレータ。

 

 





