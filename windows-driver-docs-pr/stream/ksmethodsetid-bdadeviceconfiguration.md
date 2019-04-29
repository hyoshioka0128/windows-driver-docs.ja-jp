---
title: KSMETHODSETID\_BdaDeviceConfiguration
description: KSMETHODSETID\_BdaDeviceConfiguration
ms.assetid: a0014869-2ea0-4f55-be3a-da1e624ad61c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ada463b308805a22d8fe4b6fdc28dfce4ff695e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391521"
---
# <a name="ksmethodsetidbdadeviceconfiguration"></a>KSMETHODSETID\_BdaDeviceConfiguration


## <span id="ddk_ksmethodsetid_bdadeviceconfiguration_ks"></span><span id="DDK_KSMETHODSETID_BDADEVICECONFIGURATION_KS"></span>


KSMETHODSETID\_BdaDeviceConfiguration は BDA デバイスの構成方法のセット。 フィルターのグラフのフィルターの構成に使用されます。

次の方法を使用できます。

<span id="KSMETHOD_BDA_CREATE_PIN_FACTORY"></span><span id="ksmethod_bda_create_pin_factory"></span>[**KSMETHOD\_BDA\_作成\_PIN\_ファクトリ**](ksmethod-bda-create-pin-factory.md)  
フィルターのピン留めするファクトリを作成する呼び出しをトリガーします。

<span id="KSMETHOD_BDA_DELETE_PIN_FACTORY"></span><span id="ksmethod_bda_delete_pin_factory"></span>[**KSMETHOD\_BDA\_削除\_PIN\_ファクトリ**](ksmethod-bda-delete-pin-factory.md)  
フィルターのピン留めするファクトリを削除する呼び出しをトリガーします。

<span id="KSMETHOD_BDA_CREATE_TOPOLOGY"></span><span id="ksmethod_bda_create_topology"></span>[**KSMETHOD\_BDA\_作成\_トポロジ**](ksmethod-bda-create-topology.md)  
リング 3 フィルターで既知の接続を反映するには、トポロジの構造を作成します。

### <a name="comments"></a>コメント

このメソッドのセットは、フィルターに実装されます。

BDA ミニドライバーが定義されていない場合、このメソッドのセット内のメソッドの独自のハンドラーは、BDA サポート ライブラリは、BDA ミニドライバーを呼び出すときに、既定のハンドラーに追加されます、 **BdaInitFilter**関数。

### <a name="see-also"></a>関連項目

[**BdaInitFilter**](https://msdn.microsoft.com/library/windows/hardware/ff556464)

 

 





