---
title: ミニポート アダプターとフィルター モジュールの NET_LUID 値
description: ミニポート アダプターとフィルター モジュールの NET_LUID 値
ms.assetid: d9135438-3399-4845-a28d-d445471cb41d
keywords:
- NDIS ネットワーク インターフェイス、WDK NET_LUID
- ネットワーク インターフェイス、WDK NET_LUID
- NET_LUID
- ミニポート アダプタの WDK ネットワー キング、NET_LUID 値
- フィルター モジュールの WDK ネットワー キング、NET_LUID 値
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3b92342da947c16033b14b66efaadbb5765fdca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369879"
---
# <a name="netluid-values-for-miniport-adapters-and-filter-modules"></a>NET\_ミニポート アダプターとフィルター モジュールの LUID 値





NDIS は、ミニポート ドライバー (各ミニポート アダプター) と (の各フィルター モジュール) フィルター ドライバーのためのインターフェイスを登録します。 インターフェイス インデックス NDIS を照会できますプロトコル ドライバーと[ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)ドライバーは、そのバインド ハンドルを使用してにバインドされているミニポート アダプターの値。 たとえば、MUX 中間ドライバーの下端プロトコル ドライバーを取得、NET\_LUID の値をその内部のインターフェイスの重ね順を指定します。

プロトコル ドライバーにあるバインド ハンドルを渡す、 *NdisBindingHandle*パラメーターを[ **NdisIfQueryBindingIfIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff562713)関数を受け取るインターフェイスのインデックスと NET\_上部とフィルター スタックの一番下にインターフェイスの LUID 値。 プロトコル ドライバーがこれらの値を取得する代わりに、 [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体。

ミニポート ドライバーは NDIS を NDIS ミニポート アダプタのハンドルを使用して、ミニポート アダプターのインターフェイス インデックスのクエリもできます。 ミニポート ドライバーを受け取るインターフェイス インデックスと、NET\_LUID 値、 [ **NDIS\_ミニポート\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565972)構造体。

フィルター ドライバーは、インターフェイス インデックスと、NET を取得します\_のフィルター モジュールの LUID 値、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481) 。構造体。

 

 





