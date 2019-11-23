---
title: 状態ブロックのエミュレート
description: 状態ブロックのエミュレート
ms.assetid: 1ede9f1c-f5bb-4f41-8152-63d8663fd99e
keywords:
- エミュレート状態ブロック WDK ディスプレイ
- 状態ブロックエミュレーション WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dfcd3252c13f26298dd7a9b0bcd0ef8f93c0569
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839707"
---
# <a name="emulating-state-blocks"></a>状態ブロックのエミュレート


Microsoft Direct3D ランタイムで状態ブロックをエミュレートできるようにするには、次の方法でレジストリを構成します。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Direct3D
KeyValue  : EmulateStateBlocks
ValueType : REG_DWORD
ValueData : 1 for D3D runtime emulation of stateblocks, 0 for driver implementation (default).
```

**   レジストリ**が Direct3D ランタイムによる状態ブロックのエミュレーションを有効にするように構成されている場合、ランタイムは、状態ブロック情報を設定するためにユーザーモードの表示ドライバーの[**stateset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_stateset)関数を呼び出しません。

 

 

 





