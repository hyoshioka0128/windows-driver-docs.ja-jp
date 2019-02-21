---
title: 画面の機能フラグの拡張
description: 画面の機能フラグの拡張
ms.assetid: 197d899e-57ab-40f8-9c09-440c2dc6197c
keywords:
- 拡張セキュリティ機能 WDK DirectDraw を描画するには、フラグを設定します。
- DirectDraw 拡張サーフェイス機能、Windows 2000 の WDK 表示フラグ
- 拡張セキュリティ機能 WDK DirectDraw、フラグ
- WDK の DirectDraw surface の拡張フラグを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77cc677189af22b0f734b1f6f965f0c740d282f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548619"
---
# <a name="extended-surface-capability-flags"></a>画面の機能フラグの拡張


## <span id="ddk_extended_surface_capability_flags_gg"></span><span id="DDK_EXTENDED_SURFACE_CAPABILITY_FLAGS_GG"></span>


DirectDraw の最新バージョンに追加された拡張セキュリティ機能が見られるように、ドライバー、アプリケーション適切なフラグを設定するときに、 **dwCaps2**のメンバー、 [ **DDSCAPS2**](https://msdn.microsoft.com/library/windows/hardware/ff550292)構造体。

アプリケーションでは、DDSCAPS2 を設定できますのみ\_HARDWAREDEINTERLACE フラグと共に、DDSCAPS\_オーバーレイ フラグ。 ドライバーは、このフラグに設定が表示される場合**CreateSurface**時間、DirectDraw にドライバーがデバイスのフレーム レートとハードウェアのビデオ ポート フレーム レートが一致するように必要なことすべてを行うことが期待していることを意味します。

DDSCAPS2\_HINTDYNAMIC、DDSCAPS2\_HINTSTATIC、および DDSCAPS2\_不透明なフラグはヒントにアプリケーションによって設定**CreateSurface**時間、アプリケーションのプランに、ドライバーに通知します。画面の操作を行います。 DDSCAPS2\_HINTDYNAMIC フラグは、アプリケーションが、画面を頻繁に更新があることを意味します。 DDSCAPS2\_HINTSTATIC フラグは、アプリケーションがまれには、画面が更新されますが、まだアクセスが必要です。 つまり、ドライバーは、いくつか非表示の圧縮解除、および圧縮の手順が含まれると、画面のロックを許可できる必要があります。 DDSCAPS2\_不透明なフラグは、アプリケーションが、blt をロックすることはありません、その画面の有効期間の残りの部分のサーフェイスを更新またはことを意味します。 ドライバーは圧縮または圧縮解除してこれまでしなくても、画面の順序を変更できます。

**注**  ドライバーが有効にするこれらのフラグを設定する必要はありません。 DirectDraw ドライバーにこれらのビットを渡すだけと[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)が呼び出されます。

 

ドライバー開発者は、ヒープの拡張の制限機能を使用する (で説明されている[拡張ヒープ制限](extended-heap-restrictions.md)) DirectDraw DDSCAPS2 を自動的に配置するの\_の非透過のテクスチャがヒープを最適化します。 これは、ドライバー開発者向けに完全に依存します。

DDSCAPS2\_HINTDYNAMIC、DDSCAPS2\_HINTSTATIC、および DDSCAPS2\_不透明なフラグは Microsoft DirectX ドライバー開発キット (DDK) ドキュメントで詳しく説明します。

DDSCAPS2\_TEXTUREMANAGE フラグは、ドライバーに関連することはありません。 このフラグは、ことは適切なメモリを表示するバッキング画面から、画面を移動するため、有効にする 3D テクスチャ アクセラレータを使用した DirectX のランタイムを通知します。

 

 





