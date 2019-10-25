---
title: Direct3D バージョン 9 ドライバーの DDI 変更
description: Direct3D バージョン 9 ドライバーの DDI 変更
ms.assetid: b702c02d-3be6-46e8-9e53-5d33e5e3fc70
keywords:
- Direct3d バージョン 10.1 WDK Windows 7 display、DDI の Direct3D version 9 ドライバーの変更
- Direct3D バージョン9ドライバー WDK Windows 7 ディスプレイ
- Direct3D バージョン9ドライバー WDK Windows 7 display、DDI の変更
- XR_BIAS WDK Windows 7 display、Direct3D version 9 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7433326539dd5e9da3ff2022b61d91bb371f31d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839019"
---
# <a name="ddi-changes-for-direct3d-version-9-drivers"></a>Direct3D バージョン 9 ドライバーの DDI 変更


このセクションは、Windows 7 以降のオペレーティングシステムにのみ適用されます。

XR\_BIAS は、Direct3D バージョン 9 DDI のみをサポートするユーザーモードディスプレイドライバーで Windows 7 が使用できる唯一の新しい拡張形式機能です。

このようなユーザーモードの表示ドライバーは、 [**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)列挙から D3DDDIFMT\_A2B10G10R10\_XR\_バイアス形式の値がサポートされていることを示すことができます。 ドライバーは、このようなサポートを示しています。このようなサポートは、ドライバーが[**getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数の呼び出しから返される[**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体の**pData**メンバーで、設定された[**formatop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop)構造体の配列にエントリを作成することによって示されます。D3DDDICAPS\_GETFORMATDATA 値は、D3DDDIARG の**Type**メンバー\_getcaps に設定されています。 このエントリは、 **Formatop**の**operation メンバーで**、D3DDDIFMT\_A2B10G10R10\_XR\_バイアス形式のサーフェイスでランタイムが実行できるすべての一般的な操作を示します。 たとえば、ドライバーでは、**操作**で作りビット\_の formatop\_\*設定する必要があります。 また、このドライバーでは、**操作**で formatop\_DISPLAYMODE と formatop\_3dacceleration ビットに設定する必要があります。

ドライバーが D3DDDIFMT\_A2B10G10R10\_XR\_バイアス形式の[**Formatop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop)エントリを返した場合、ドライバーはその[**createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数の呼び出しを受け取って、D3DDDIFMT を使用してリソースを作成することができ\_A2B10G10R10\_XR は、 [**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**format**メンバーで設定された\_バイアス形式です。

ドライバーは、全画面の反転チェーンに対して、D3DDDIFMT\_A2B10G10R10\_XR\_バイアス形式でリソースを作成する要求のみを受信します。 デスクトップ Windows マネージャー (DWM) は、シェーダーコードの XR\_バイアスのウィンドウ表示を処理します。 ドライバーは、D3DDDIFMT\_A2B10G10R10\_XR\_バイアス形式リソースを、スキャンアウトを除くすべての操作で D3DDDIFMT\_A2B10G10R10 形式として扱う必要があります。たとえば、ドライバーは D3DDDIFMT\_A2B10G10R10 を扱うことができ\_XR\_バイアス-リソースを D3DDDIFMT\_A2B10G10R10 形式として書式設定して、ブレンド、フィルター処理、および書式変換操作を実行します。 唯一の違いは、XR\_バイアスがスキャンアウトに与える影響です。スキャンアウトの詳細については、「 [Bgra Scan Out Support](bgra-scan-out-support.md)」を参照してください。

 

 





