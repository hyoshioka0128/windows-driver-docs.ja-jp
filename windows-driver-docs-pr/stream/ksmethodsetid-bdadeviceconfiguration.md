---
title: KSMETHODSETID\_BdaDeviceConfiguration
description: KSMETHODSETID\_BdaDeviceConfiguration
ms.assetid: a0014869-2ea0-4f55-be3a-da1e624ad61c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1b44ce62c6503a8e9c167d4abb47a08c143d97b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842414"
---
# <a name="ksmethodsetid_bdadeviceconfiguration"></a>KSMETHODSETID\_BdaDeviceConfiguration


## <span id="ddk_ksmethodsetid_bdadeviceconfiguration_ks"></span><span id="DDK_KSMETHODSETID_BDADEVICECONFIGURATION_KS"></span>


KSMETHODSETID\_BdaDeviceConfiguration は、BDA デバイス構成メソッドセットです。 フィルターグラフのフィルターを構成するために使用されます。

次の方法を使用できます。

<span id="KSMETHOD_BDA_CREATE_PIN_FACTORY"></span><span id="ksmethod_bda_create_pin_factory"></span>[**KSK メソッド\_BDA\_作成\_PIN\_ファクトリ**](ksmethod-bda-create-pin-factory.md)  
フィルターの pin ファクトリを作成する呼び出しをトリガーします。

<span id="KSMETHOD_BDA_DELETE_PIN_FACTORY"></span><span id="ksmethod_bda_delete_pin_factory"></span>[**KSK メソッド\_BDA\_削除\_\_ファクトリ**](ksmethod-bda-delete-pin-factory.md)  
フィルターの pin ファクトリを削除する呼び出しをトリガーします。

<span id="KSMETHOD_BDA_CREATE_TOPOLOGY"></span><span id="ksmethod_bda_create_topology"></span>[**KSK メソッド\_BDA\_\_トポロジを作成します**](ksmethod-bda-create-topology.md)  
フィルター内の既知の接続を反映するトポロジ構造をリング3に作成します。

### <a name="comments"></a>コメント

このメソッドセットは、フィルターに実装されています。

このメソッドセット内のメソッドに対して、BDA ミニドライバーが独自のハンドラーを定義していない場合、bda サポートライブラリは、BDA ミニドライバーが**BdaInitFilter**関数を呼び出したときに既定のハンドラーを追加します。

### <a name="see-also"></a>参照

[**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)

 

 





