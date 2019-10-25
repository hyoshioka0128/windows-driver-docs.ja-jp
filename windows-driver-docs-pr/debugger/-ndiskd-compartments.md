---
title: ndiskd コンパートメント
description: Ndiskd コンパートメント拡張子は、すべてのネットワークコンパートメントを表示します。
ms.assetid: F9BF319D-77E9-4D12-84E9-655058F57AC4
keywords:
- ndiskd コンパートメント Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.compartments
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b13462322d9c3e505d49dfee52f7ddc3baad8bea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837600"
---
# <a name="ndiskdcompartments"></a>!ndiskd.compartments


**! Ndiskd コンパートメント**拡張子は、すべてのネットワークコンパートメントを表示します。

```console
!ndiskd.compartments 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


この拡張機能にはパラメーターがありません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="remarks"></a>注釈
-------

コンパートメントは、NDIS がインターフェイスを管理する方法です。 サードパーティのインターフェイスプロバイダーは、 [**NDIS\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体に関するページで説明**されて**いるように、プライマリコンパートメントのみを使用します。

<a name="examples"></a>例
--------

**! Ndiskd コンパートメント**拡張機能を実行して、すべてのネットワークコンパートメントの一覧を表示します。 この例では、コンパートメントが1つ (プライマリプライマリ) だけです。

```console
3: kd> !ndiskd.compartments
    Compartment        ffffdf80139b9940
    ID                 1
    Loopback Network   ffffdf80139b8900
    Loopback Interface ffffdf80139b6a20
    Networks:
                       ffffdf80139b8900    [Unnamed network]
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **! ndiskd ヘルプ**](-ndiskd-help.md)

[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

 

 






