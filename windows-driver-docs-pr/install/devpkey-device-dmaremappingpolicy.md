---
title: DEVPKEY_Device_DmaRemappingPolicy
description: DEVPKEY_Device_DmaRemappingPolicy
ms.assetid: 3553debf-dec8-4135-9bd7-6ce2941afa52
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_DmaRemappingPolicy
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DmaRemappingPolicy
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 07/15/2020
ms.openlocfilehash: f53b7c0810291b05f3c57f32ad12760fb31a251b
ms.sourcegitcommit: 1ab8fc6d15fac78ce243f3852d86733ebfca40dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86436889"
---
# <a name="devpkey_device_dmaremappingpolicy"></a>DEVPKEY_Device_DmaRemappingPolicy

DEVPKEY_Device_DmaRemappingPolicy デバイスプロパティの値は、デバイスの DMA 再マップ機能を示します。

**プロパティキー**: DEVPKEY_Device_DmaRemappingPolicy  
**プロパティ-データ型識別子**: [ **DEVPROP_TYPE_INT32**](devprop-type-int32.md)  
**プロパティアクセス**: アプリケーションとサービスによる読み取り専用アクセス。  
**ローカライズ**された場合: いいえ  

 
<a name="remarks"></a>解説
-------

| 値 | 意味 |
| ----- | ------- |
| 2     | このデバイスのドライバーは、DMA の再マップを使用できます。 |
| 1     | このデバイスの少なくとも1つのドライバーによって、DMA の再マップが除外されています。 |
| 0または DMA の再マップポリシープロパティは表示されません | DMA 再マップ INF ディレクティブが INF ファイルで指定されていません。 このデバイスには DMA の再マップは適用されません。 |


[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)と[**setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)を呼び出すことによって、DEVPKEY_Device_DmaRemappingPolicy プロパティにアクセスできます。

<a name="requirements"></a>必要条件
------------

**バージョン**: Windows 10 バージョン1803で使用可能 (redstone 4)  
**ヘッダー**: Devpkey (Devpkey を含む)  


## <a name="see-also"></a>関連項目

[デバイスドライバーの DMA 再マップの有効化](../pci/enabling-dma-remapping-for-device-drivers.md)

[カーネル DMA 保護](https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)


