---
title: KSPROPSETID\_BdaPinControl
description: KSPROPSETID\_BdaPinControl
ms.assetid: f3c6ae83-d50f-49c8-a851-763f191f1932
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f365c182efe38f6edd5097fa18fe2a4e913308b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384493"
---
# <a name="kspropsetidbdapincontrol"></a>KSPROPSETID\_BdaPinControl


## <span id="ddk_kspropsetid_bdapincontrol_ks"></span><span id="DDK_KSPROPSETID_BDAPINCONTROL_KS"></span>


KSPROPSETID\_BdaPinControl は BDA 暗証番号 (pin) のコントロールのプロパティ セット。 特定の pin に関する BDA 固有情報を取得に使用されます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_PIN_ID"></span><span id="ksproperty_bda_pin_id"></span>[**KSPROPERTY\_BDA\_PIN\_ID**](ksproperty-bda-pin-id.md)  
Pin の BDA 識別子 (ID) を返します。

<span id="KSPROPERTY_BDA_PIN_TYPE"></span><span id="ksproperty_bda_pin_type"></span>[**KSPROPERTY\_BDA\_PIN\_型**](ksproperty-bda-pin-type.md)  
Pin の種類を示す値を返します。

### <a name="comments"></a>コメント

ネットワークの後に、プロバイダーは、KSMETHOD を使用してフィルターの暗証番号 (pin) を作成します\_BDA\_作成\_PIN\_FACTORY 要求は、KSMETHODSETID の\_BdaDeviceConfiguration メソッドのセット、ネットワーク プロバイダー。KSPROPSETID のプロパティを使用して\_BdaPinControl を実際の受信者のトポロジの内部表現を更新します。

BDA フィルターの各ピンの工場出荷時に、このプロパティを設定をサポートする必要があります。 BDA ミニドライバーは、このプロパティを設定を定義していないかどうかは、BDA サポート ライブラリがいずれかで、ピン留めするファクトリの作成時に、サポートを追加、 **BdaCreatePin**または**BdaInitFilter**関数。

このプロパティのプロパティは、戻り値については、pin を設定します。 通常、フィルターのピンは、これらのプロパティのいずれか傍受する必要はありません。 BDA サポート ライブラリには、 **BdaPropertyGetPinControl**既定のこのプロパティのセットを処理する関数。

### <a name="see-also"></a>関連項目

[**BdaCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdacreatepin), [**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdainitfilter), [**BdaPropertyGetPinControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertygetpincontrol), [KSMETHODSETID\_BdaDeviceConfiguration](ksmethodsetid-bdadeviceconfiguration.md)

 

 





