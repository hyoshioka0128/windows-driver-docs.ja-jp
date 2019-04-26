---
title: Direct3D バージョン 9 ドライバーの DDI 変更
description: Direct3D バージョン 9 ドライバーの DDI 変更
ms.assetid: b702c02d-3be6-46e8-9e53-5d33e5e3fc70
keywords:
- Direct3D のバージョン 9 ドライバーの Direct3D バージョン 10.1 WDK Windows 7 の表示、DDI の変更します。
- Direct3D のバージョン 9 ドライバー WDK Windows 7 を表示します。
- Direct3D のバージョン 9 ドライバー WDK Windows 7 の表示、DDI の変更します。
- XR_BIAS WDK Windows 7 の表示、Direct3D のバージョン 9 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daeb1c81340810f5c59fbc9439aad7971fbdfc79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341527"
---
# <a name="ddi-changes-for-direct3d-version-9-drivers"></a>Direct3D バージョン 9 ドライバーの DDI 変更


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

XR\_バイアスは、Windows 7 にのみ、Direct3D のバージョン 9 をサポートするユーザー モードのディスプレイ ドライバーを使用できるように書式設定機能を拡張のみ新しい DDI します。

このようなユーザー モードのディスプレイ ドライバーは、D3DDDIFMT をサポートしていることを示すことができます\_A2B10G10R10\_XR\_バイアス形式の値から、 [ **D3DDDIFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff544312)列挙体です。 ドライバーでは、このようなサポートを示すの配列内のエントリを作成して設定された[ **FORMATOP** ](https://msdn.microsoft.com/library/windows/hardware/ff566438)内の構造体、 **pData**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)構造体への呼び出しからドライバーを返す、 [ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762) D3DDDICAPS で関数を\_GETFORMATDATA 値の設定、**型**D3DDDIARG のメンバー\_GETCAPS します。 このエントリを示すため、**操作**のメンバー **FORMATOP**、すべてのランタイムは、D3DDDIFMT とサーフェスで実行できる一般的な操作\_A2B10G10R10\_XR\_バイアス形式。 たとえば、ドライバーは、FORMATOP を設定する必要があります\_\*\_レンダリング ターゲットのビットで**操作**します。 ドライバーは、FORMATOP を設定する必要がありますも\_DISPLAYMODE と FORMATOP\_3DACCELERATION ビットで**操作**します。

ドライバーが返された場合、 [ **FORMATOP** ](https://msdn.microsoft.com/library/windows/hardware/ff566438)エントリ、D3DDDIFMT\_A2B10G10R10\_XR\_バイアス形式、その後、ドライバーはそのへの呼び出しを受信します。[**CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688) 、D3DDDIFMT のリソースを作成する関数\_A2B10G10R10\_XR\_バイアス形式の設定、**形式**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)構造体。

ドライバーのみ、D3DDDIFMT のリソースを作成する要求を受信する\_A2B10G10R10\_XR\_フリッピング チェーンの全画面表示のバイアス形式。 Windows デスクトップ マネージャー (DWM) XR のウィンドウのプレゼンテーションを処理する\_シェーダー コードのバイアス。 ドライバーが D3DDDIFMT を扱う必要があります\_A2B10G10R10\_XR\_バイアス形式のリソースとして、D3DDDIFMT\_A2B10G10R10 がスキャンを除くすべての操作で書式設定、ドライバーが D3DDDIFMT を扱うことができます、\_A2B10G10R10\_XR\_バイアス形式のリソースとして、D3DDDIFMT\_ブレンド、フィルター、および形式変換の操作の A2B10G10R10 形式。 唯一の違いはどのように XR\_バイアス スキャン アウトに影響を与えます。スキャン アウトの詳細については、次を参照してください。 [BGRA スキャン アウト サポート](bgra-scan-out-support.md)します。

 

 





