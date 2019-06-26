---
title: DirectX VA デコードの設定
description: DirectX VA デコードの設定
ms.assetid: 8841c366-df00-4e88-9f50-85345ba77e03
keywords:
- ビデオのデコード WDK DirectX va なので、設定します。
- ビデオの WDK DirectX va なので、セットアップのデコード
- デコード WDK DirectX va なので、設定の画像します。
- ビデオのデコード WDK DirectX va なので、書式設定します。
- ビデオの WDK DirectX va なので、形式のデコード
- WDK の DirectX va なので、形式をデコードする画像
- WDK DirectX VA を書式設定します。
- デコードの WDK DirectX VA を画像します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9b00f5c86a682745c2a1c853b57710c668d233a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365521"
---
# <a name="setting-up-directx-va-decoding"></a>DirectX VA デコードの設定


## <span id="ddk_setting_up_directx_va_decoding_gg"></span><span id="DDK_SETTING_UP_DIRECTX_VA_DECODING_GG"></span>


デコーダー アクセラレータで正常に動作するためには、デコーダーとアクセラレータを操作の 2 つの側面に設定する必要があります。

-   デコードするビデオ データ形式。 [ **DXVA\_ConnectMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_connectmode)構造を使用して形式を指定します。

-   ホストとアクセラレータ間のデータ交換に使用され、アクセラレータ上で、ホストとするが存在するプロセスを確立する形式を決定する構成。 この構成は、接続の構成を使用するには、各 DirectX VA 関数のネゴシエーションで確立されます (によって決定される、 [bDXVA\_Func](bdxva-func-variable.md)変数)。 [ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)構造体は、構成を指定します。

 

 





