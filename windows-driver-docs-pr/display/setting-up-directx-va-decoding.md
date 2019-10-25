---
title: DirectX VA デコードの設定
description: DirectX VA デコードの設定
ms.assetid: 8841c366-df00-4e88-9f50-85345ba77e03
keywords:
- ビデオデコード WDK DirectX VA、セットアップ
- video WDK DirectX VA のデコード、セットアップ
- 画像デコード WDK DirectX VA、セットアップ
- ビデオデコード WDK DirectX VA、形式
- ビデオのデコード (WDK DirectX VA、形式)
- 画像デコード WDK DirectX VA、形式
- WDK DirectX VA の形式
- 画像デコード WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cfa24891c48f5ce5f7216db665b958bbf4e1eea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825792"
---
# <a name="setting-up-directx-va-decoding"></a>DirectX VA デコードの設定


## <span id="ddk_setting_up_directx_va_decoding_gg"></span><span id="DDK_SETTING_UP_DIRECTX_VA_DECODING_GG"></span>


デコーダーがアクセラレータを使用して正しく動作するためには、次の2つの操作の側面についてデコーダーとアクセラレータがセットアップされている必要があります。

-   デコードするビデオデータの形式。 [**DXVA\_ConnectMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)構造体は、形式を指定するために使用されます。

-   ホストとアクセラレータ間のデータ交換に使用される形式を決定し、ホストとアクセラレータに存在するプロセスを確立する構成。 この構成は、( [bDXVA\_Func](bdxva-func-variable.md)変数によって決定されるように) 使用される各 DirectX VA 関数の接続構成のネゴシエーションによって確立されます。 [**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体は、構成を指定します。

 

 





