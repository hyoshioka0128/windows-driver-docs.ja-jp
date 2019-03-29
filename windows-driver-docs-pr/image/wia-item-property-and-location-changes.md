---
title: WIA 項目のプロパティと場所の変更
description: WIA 項目のプロパティと場所の変更
ms.assetid: 4e8b3d2a-a28c-41d1-9c4b-8d85f28cf904
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc3b7b622b1070bfcc29828839480a50a6f83da3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579146"
---
# <a name="wia-item-property-and-location-changes"></a>WIA 項目のプロパティと場所の変更





Windows Vista と以前のオペレーティング システムでアプリケーションの互換性を確保する最も簡単な方法は、Windows XP と Windows Me の場所で、WIA プロパティを実装するために、*と*Windows Vista の場所にします。 Windows Vista 向けに作成された WIA アプリケーションを WIA プロパティと、WIA プロパティとは場所でのみ機能しますが記述されているアプリケーションの Windows XP および Windows Me、Windows vista の場合、追加の場所でのみ動作する通常は、これらのオペレーティング システムで定義されます。 Windows Vista、Windows XP、および Windows Me と同じプロパティ セットの実装を使用するために記述されているアプリケーションは、両方の場所でプロパティを実装できます。

Windows Vista より前に、のオペレーティング システムで、次の WIA プロパティは、フラット ベッドからプラテン上のスキャンがサポートされているスキャナー ドライバーのルート項目に配置されていた。 Windows Vista で、フラット ベッド項目に配置されています。

-   [**WIA\_DPS\_水平\_ベッド\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551399) (と呼ばれる[ **WIA\_IP\_最大\_水平\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff552607) Windows vista)

-   [**WIA\_DPS\_垂直\_ベッド\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551445) (と呼ばれる[ **WIA\_IP\_最大\_垂直\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff552611) Windows vista)

-   [**WIA\_DPS\_光\_XRES** ](https://msdn.microsoft.com/library/windows/hardware/ff551409) (と呼ばれる[ **WIA\_IP\_光\_XRES** ](https://msdn.microsoft.com/library/windows/hardware/ff552620)Windows vista)

-   [**WIA\_DPS\_光\_YRES** ](https://msdn.microsoft.com/library/windows/hardware/ff551410) (と呼ばれる[ **WIA\_IP\_光\_YRES** ](https://msdn.microsoft.com/library/windows/hardware/ff552622)Windows vista)

-   [**WIA\_DPS\_プレビュー** ](https://msdn.microsoft.com/library/windows/hardware/ff551422) (と呼ばれる[ **WIA\_IP\_プレビュー** ](https://msdn.microsoft.com/library/windows/hardware/ff552643) Windows vista)

-   [**WIA\_DPS\_表示\_プレビュー\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff551432) (と呼ばれる[ **WIA\_IP\_表示\_プレビュー\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff552652) Windows vista)

**注**   WIA プロパティの重複がフラット ベッドからプラテン上のスキャンまたはドキュメント フィーダーのスキャンをサポートするスキャナーにのみ必要です。 ペアになっているプロパティがある互換性のための同じプロパティ識別子。 ドライバーは、WIA を追加できます\_DPS\_*Xxx*プロパティをルート項目と WIA\_IP\_*Xxx*他のアイテム。

 

 

 




