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
ms.openlocfilehash: 11eddc11d46148060cdb8c0c35afbcbc4e9cce02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573067"
---
# <a name="setting-up-directx-va-decoding"></a>DirectX VA デコードの設定


## <span id="ddk_setting_up_directx_va_decoding_gg"></span><span id="DDK_SETTING_UP_DIRECTX_VA_DECODING_GG"></span>


デコーダー アクセラレータで正常に動作するためには、デコーダーとアクセラレータを操作の 2 つの側面に設定する必要があります。

-   デコードするビデオ データ形式。 [ **DXVA\_ConnectMode** ](https://msdn.microsoft.com/library/windows/hardware/ff563138)構造を使用して形式を指定します。

-   ホストとアクセラレータ間のデータ交換に使用され、アクセラレータ上で、ホストとするが存在するプロセスを確立する形式を決定する構成。 この構成は、接続の構成を使用するには、各 DirectX VA 関数のネゴシエーションで確立されます (によって決定される、 [bDXVA\_Func](bdxva-func-variable.md)変数)。 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体は、構成を指定します。

 

 





