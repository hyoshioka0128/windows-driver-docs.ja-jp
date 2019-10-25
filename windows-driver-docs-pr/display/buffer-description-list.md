---
title: バッファーの説明の一覧
description: バッファーの説明の一覧
ms.assetid: 7d820491-2df2-4036-8f3d-e6bcff4cd1f6
keywords:
- ビデオデコード WDK DirectX VA、バッファー説明リスト
- ビデオをデコードしています。 WDK DirectX VA、バッファー説明リスト
- 画像デコード WDK DirectX VA、バッファー説明リスト
- バッファー WDK DirectX VA
- バッファーの説明リスト WDK DirectX VA
- DXVA_BufferDescription
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30a7c5d74f77dee064cc325077ace65d55788f8a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839823"
---
# <a name="buffer-description-list"></a>バッファーの説明の一覧


## <span id="ddk_buffer_description_list_gg"></span><span id="DDK_BUFFER_DESCRIPTION_LIST_GG"></span>


DirectX VA は、主にホストデコーダーからのデータバッファーをハードウェアアクセラレータに渡すことによって動作します。 バッファーのセットがホストからアクセラレータに渡されると、バッファーの説明リストが送信されてバッファーが記述されます。 バッファーの説明リストは、 [**DXVA\_BufferDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)構造体の配列です。 バッファーの説明の一覧には、送信されるバッファーセット内の各バッファーの DXVA\_BufferDescription 構造体が1つ含まれています。 バッファーの説明の一覧は、最初に送信されるバッファーの種類に対して1つ以上の DXVA\_BufferDescription 構造体で始まります。 これに続いて、次の種類のバッファーに送信されるバッファーの DXVA\_BufferDescription 構造体が1つ以上続きます。

[**DXVA\_BufferDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)構造体の**dwtypeindex**メンバーの値は、ホストからアクセラレータに渡されるバッファーの種類を指定します。

 

 





