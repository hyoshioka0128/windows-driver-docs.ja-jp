---
title: 拡張形式の認識のサポート
description: 拡張形式の認識のサポート
ms.assetid: b473ebf2-75a0-4e3f-8190-d1a557ae6da0
keywords:
- Direct3D のバージョン 10.1 WDK Windows 7 の表示
- 拡張形式の認識、Direct3D バージョン 10.1 WDK Windows 7 表示
- 拡張形式認識 WDK Windows 7 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a54a7815037d84009221ab2dc2309a3e144e0f95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372752"
---
# <a name="supporting-extended-format-awareness"></a>拡張形式の認識のサポート


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

Windows 7 を提供する Direct3D 10.1 のバージョンについては、いくつかの新しい形式が定義されます。 また、Windows 7 の Direct3D 10.1 には、DXGI\_形式\_R8G8B8A8\_型の既存形式ファミリのメンバー間でキャストすることができます。 Direct3D 10.1 以降、新しいバージョンとハードウェアの機能の検出メカニズムを介してこの拡張形式のサポートを公開します。 Direct3D 10.0 では、グラフィックス ハードウェアに Direct3D 10.1 機能がある場合でも、拡張の形式はサポートしません。

以下は、拡張形式の認識をサポートする Direct3D 10.1 の新機能です。

-   新しい XR ハイカラー スキャン アウト形式します。

-   Direct3D のバージョン 10 から不足しているフォーマット BGR を再度追加します。

-   DXGI の完全に型指定されたメンバーの異なる方法で書式設定されたビューの作成を有効にする\_形式\_R8G8B8A8\_TYPELESS、DXGI\_形式\_R10G10B10A2\_TYPELESS と DXGI\_形式\_R16G16B16\_A16\_型宣言不要なファミリは、すべての Direct3D バージョン 10 スキャン アウト形式を含む

-   スキャン アウトと BGRA および BGRA のサポートを提示\_SRGB

Windows 7 には、DWM に通信するために 10:10:10:2 バック バッファーの XR の解釈を許可する新しいスワップ チェーン フラグの Direct3D 9 のバージョンも提供します。

次のセクションでは、Direct3D の新機能について説明します。

[バージョンの検出のサポート](version-discovery-support.md)

[拡張形式の詳細](details-of-the-extended-format.md)

[完全に型指定されたキャスト バック バッファー](fully-typed-back-buffers-casting.md)

[BGRA スキャン アウトのサポート](bgra-scan-out-support.md)

[形式の対応要件の拡張](extended-format-aware-requirements.md)

[Direct3D のバージョン 9 ドライバー DDI 変更](ddi-changes-for-direct3d-version-9-drivers.md)

 

 





