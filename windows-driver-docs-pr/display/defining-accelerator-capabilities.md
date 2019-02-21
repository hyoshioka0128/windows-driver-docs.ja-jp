---
title: アクセラレータの機能を定義します。
description: アクセラレータの機能を定義します。
ms.assetid: 1f590cfd-74b8-4a08-848d-fcbb2c0c9486
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、アクセラレータの機能
- ビデオ アクセラレータ WDK DirectX、アクセラレータの機能
- VA WDK DirectX、アクセラレータの機能
- 制限付きプロファイル WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b6751a906b48c22c4bc989e962a7bc658c4cd37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558616"
---
# <a name="defining-accelerator-capabilities"></a>アクセラレータの機能を定義します。


## <span id="ddk_defining_accelerator_capabilities_gg"></span><span id="DDK_DEFINING_ACCELERATOR_CAPABILITIES_GG"></span>


制限付きの操作で使用できるアクセラレータに準拠している場合、[プロファイルを制限](restricted-profiles.md)、nonrestricted 操作で使用できますか場合、制限付きのプロファイルに準拠していません。

### <a name="span-idrestrictedoperationspanspan-idrestrictedoperationspanspan-idrestrictedoperationspanrestricted-operation"></a><span id="Restricted_Operation"></span><span id="restricted_operation"></span><span id="RESTRICTED_OPERATION"></span>制限付きの操作

アクセラレータの機能は、サポートされる制限されたプロファイルに従って定義されます。 アクセラレータは、1 つまたは複数の制限プロファイルをサポート可能性があります。

他の制限プロファイルの機能のサブセットとして定義されているいくつか制限付きのプロファイル (MPEG2 など\_プロファイルは、MPEG2 の機能のサブセット\_B プロファイル)。 特定の制限プロファイルをサポートするアクセラレータはサポートされているプロファイルのサブセットである任意の制限プロファイルもサポートする必要があります。 MPEG2 をサポートするアクセラレータなど\_B プロファイルは、MPEG2 をサポートする必要がありますも\_プロファイル。

### <a name="span-idnonrestrictedoperationspanspan-idnonrestrictedoperationspanspan-idnonrestrictedoperationspannonrestricted-operation"></a><span id="Nonrestricted_Operation"></span><span id="nonrestricted_operation"></span><span id="NONRESTRICTED_OPERATION"></span>Nonrestricted 操作

DirectX VA で、アクセラレータを使用せずに制限されているプロファイルでは、厳密に準拠している場合、 **wRestrictedMode**のメンバー、 [ **DXVA\_ConnectMode** ](https://msdn.microsoft.com/library/windows/hardware/ff563138)構造体は、制限のこのがないことを示す 0 xffff に設定する必要があります。

すべての値が定義されている、 **bDXVA\_Func**変数が許可されます。

 

 





