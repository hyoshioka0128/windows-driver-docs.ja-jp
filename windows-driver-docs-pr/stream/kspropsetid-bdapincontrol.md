---
title: KSPROPSETID\_BdaPinControl
description: KSPROPSETID\_BdaPinControl
ms.assetid: f3c6ae83-d50f-49c8-a851-763f191f1932
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a141a911a42e6196b2196acaab2a714b4425b3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845627"
---
# <a name="kspropsetid_bdapincontrol"></a>KSPROPSETID\_BdaPinControl


## <span id="ddk_kspropsetid_bdapincontrol_ks"></span><span id="DDK_KSPROPSETID_BDAPINCONTROL_KS"></span>


KSPROPSETID\_BdaPinControl は、BDA ピン制御プロパティセットです。 特定の pin に関するいくつかの BDA 固有の情報を取得するために使用されます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_PIN_ID"></span><span id="ksproperty_bda_pin_id"></span>[**KSK プロパティ\_BDA\_PIN\_ID**](ksproperty-bda-pin-id.md)  
ピンの BDA 識別子 (ID) を返します。

<span id="KSPROPERTY_BDA_PIN_TYPE"></span><span id="ksproperty_bda_pin_type"></span>[**KSK プロパティ\_BDA\_PIN\_型**](ksproperty-bda-pin-type.md)  
ピンの種類を指定する値を返します。

### <a name="comments"></a>コメント

ネットワークプロバイダーが KSK メソッドを使用してフィルターの pin を作成した後\_BDA\_KSK METHODSETID\_BdaDeviceConfiguration\_\_のファクトリ要求を作成し、ネットワークプロバイダーはのプロパティを使用します。KSPROPSETID\_BdaPinControl は、実際の受信者トポロジの内部表現を更新します。

BDA フィルターの各ピンファクトリは、このプロパティセットをサポートする必要があります。 BDA ミニドライバーでこのプロパティセットが定義されていない場合は、ピンファクトリが**Bdacreatepin**または**BdaInitFilter**関数によって作成されるときに、bda サポートライブラリによってサポートが追加されます。

このプロパティセットのプロパティは、pin に関する情報を返します。 通常、フィルターのピンは、これらのプロパティのいずれかをインターセプトする必要がありません。 BDA サポートライブラリには、このプロパティセットを処理する**Bdapropertygetpincontrol** default 関数が用意されています。

### <a name="see-also"></a>参照

[**Bdacreatepin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatepin)、 [**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)、 [**bdapropertygetpincontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertygetpincontrol)、 [ksmethodsetid\_bdadevic](ksmethodsetid-bdadeviceconfiguration.md)

 

 





