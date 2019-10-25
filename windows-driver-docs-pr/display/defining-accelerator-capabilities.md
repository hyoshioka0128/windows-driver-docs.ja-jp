---
title: アクセラレータ機能の定義
description: アクセラレータ機能の定義
ms.assetid: 1f590cfd-74b8-4a08-848d-fcbb2c0c9486
keywords:
- DirectX ビデオアクセラレータ WDK Windows 2000 ディスプレイ、アクセラレータ機能
- ビデオアクセラレーション WDK DirectX、アクセラレータ機能
- VA WDK DirectX、アクセラレータ機能
- 制限されたプロファイル WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7d1638a64d80e1e3003bbbd8637c75b3af6f9f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839765"
---
# <a name="defining-accelerator-capabilities"></a>アクセラレータ機能の定義


## <span id="ddk_defining_accelerator_capabilities_gg"></span><span id="DDK_DEFINING_ACCELERATOR_CAPABILITIES_GG"></span>


アクセラレータは制限された操作で使用できます。この場合、制限付き[プロファイル](restricted-profiles.md)に準拠しているか、制限されていない操作で使用できます。この場合、制限付きプロファイルに準拠していません。

### <a name="span-idrestricted_operationspanspan-idrestricted_operationspanspan-idrestricted_operationspanrestricted-operation"></a><span id="Restricted_Operation"></span><span id="restricted_operation"></span><span id="RESTRICTED_OPERATION"></span>制限された操作

アクセラレータの機能は、サポートする制限プロファイルに応じて定義されます。 アクセラレータは、1つまたは複数の制限されたプロファイルをサポートする場合があります。

制限されたプロファイルの中には、他の制限付きプロファイルの機能のサブセットとして定義されているものがあります (たとえば、MPEG2\_プロファイルは、MPEG2\_B プロファイルの機能のサブセットです)。 特定の制限されたプロファイルをサポートするアクセラレータでは、サポートされているプロファイルのサブセットである制限されたプロファイルもサポートする必要があります。 たとえば、MPEG2\_B プロファイルをサポートするアクセラレータでは、MPEG2\_プロファイルもサポートしている必要があります。

### <a name="span-idnonrestricted_operationspanspan-idnonrestricted_operationspanspan-idnonrestricted_operationspannonrestricted-operation"></a><span id="Nonrestricted_Operation"></span><span id="nonrestricted_operation"></span><span id="NONRESTRICTED_OPERATION"></span>非制限演算

DirectX VA で、制限されたプロファイルに厳密に準拠せずにアクセラレータを使用する場合は、制限がないことを示すために、 [**DXVA\_ConnectMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)構造体の**WRestrictedMode**メンバーを0xffff に設定する必要があります。

**BDXVA\_Func**変数に定義されているすべての値が許可されます。

 

 





