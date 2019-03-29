---
title: Direct3D バージョン 10 カーネル ハンドル
description: Direct3D バージョン 10 カーネル ハンドル
ms.assetid: 48378f27-4c08-4931-9592-878a1a2b2556
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a791f97207085246cbc82549022fbb20f4b4b10f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580385"
---
# <a name="direct3d-version-10-kernel-handles"></a>Direct3D バージョン 10 カーネル ハンドル


一般に、ユーザー モードのディスプレイ ドライバーによっては Direct3D バージョン 10 カーネル ハンドルの有効期限は明示的に制御されます。 このようなハンドルの割り当てを操作するユーザー モードのディスプレイ ドライバーを許可します。 このような処理は、(ディスプレイのミニポート ドライバーとの対話を含む)、カーネルを他の操作を実行するユーザー モードのディスプレイ ドライバーもできます。

リソースのカーネル ハンドルの例を次に示します。

```cpp
// Strongly typed handle to identify a resource object to the driver: 
typedef struct D3D10DDI_HKMRESOURCE
{
    D3DKMT_HANDLE handle;
} D3D10DDI_HKMRESOURCE;
```

 

 





