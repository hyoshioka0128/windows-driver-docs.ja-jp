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
ms.openlocfilehash: 6a6b868bb046f15631c60c8a32d723566390d2dd
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534741"
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

コンパートメントは、NDIS がインターフェイスを管理する方法です。 サードパーティのインターフェイスプロバイダーは、 [**NDIS \_ バインド \_ パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体の**CompartmentId**メンバーで説明されているように、プライマリコンパートメントのみを使用します。

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


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NDIS \_ バインド \_ パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

 

 






