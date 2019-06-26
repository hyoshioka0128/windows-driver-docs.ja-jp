---
title: バッファー情報リスト
description: バッファー情報リスト
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
ms.openlocfilehash: 6cb2ad32b655e23fdf1342d55d42fcbebbd78a45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384616"
---
# <a name="buffer-description-list"></a>バッファー情報リスト


## <span id="ddk_buffer_description_list_gg"></span><span id="DDK_BUFFER_DESCRIPTION_LIST_GG"></span>


DirectX VA は、主に、ホスト デコーダーから、ハードウェア アクセラレータにデータのバッファーを渡すことによって動作します。 アクセラレータにホストからのバッファー セットが渡されるバッファーを記述するバッファーの説明の一覧が送信されます。 バッファーの説明の一覧は、配列の[ **DXVA\_BufferDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_bufferdescription)構造体。 バッファーの説明の一覧には、1 つの DXVA が含まれています。\_送信されるバッファーのセット内の各バッファーの BufferDescription 構造体。 バッファーの説明の一覧から 1 つまたは複数の DXVA 始まります\_BufferDescription 構造体が送信されるバッファーの最初の型。 これは、後に 1 つまたは複数の DXVA\_BufferDescription 構造体が送信されるバッファーの次の種類。

値、 **dwTypeIndex**のメンバー、 [ **DXVA\_BufferDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_bufferdescription)構造体は、ホストから渡されるバッファーの種類を指定します、アクセラレータ。

 

 





