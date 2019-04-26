---
title: 最適化された画面回転のサポート
description: Windows 8 では、回転モードの変更中にグラフィックス アダプターからの出力を有効なままことを確認して、ちらつきのない画面の回転のエクスペリエンスを保証します。
ms.assetid: CFDB4713-EC90-4FAB-B379-742C52888BB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5daba1898d782332cd91d0a7922a3215128ffad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358365"
---
# <a name="optimized-screen-rotation-support"></a>最適化された画面回転のサポート


Windows 8 では、回転モードの変更中にグラフィックス アダプターからの出力を有効なままことを確認して、ちらつきのない画面の回転のエクスペリエンスを保証します。 この機能は、回転のモードをサポートするすべての Windows Display Driver Model (WDDM) 1.2 ドライバーに必要です。

**注**  デバイス ドライバー インターフェイス (Ddi) は Windows 8.1 Update 以降、プライマリ ディスプレイを回転したときに、複製されたモニターの最も高い解像度をサポートするために更新されます。 参照してください[パスに依存しない回転をサポートしている](supporting-path-independent-rotation.md)します。

 

|                                                      |           |
|------------------------------------------------------|-----------|
| WDDM の最小バージョン                                 | 1.2       |
| Windows の最小バージョン                              | 8         |
| ドライバーの実装: 完全なグラフィックスおよび表示のみ | 必須 |

 

## <a name="span-idsmoothrotationddispanspan-idsmoothrotationddispanspan-idsmoothrotationddispansmooth-rotation-ddi"></a><span id="Smooth_rotation_DDI"></span><span id="smooth_rotation_ddi"></span><span id="SMOOTH_ROTATION_DDI"></span>滑らかな回転 DDI


ディスプレイのミニポート ドライバーでは、これらのドライバー実装関数を呼び出すときに、パスの回転を更新をサポートする必要があります。

-   [*DxgkDdiCommitVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559597)
-   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://msdn.microsoft.com/library/windows/hardware/ff560803)

ドライバーへの呼び出しで滑らかな回転のサポートを指定する必要があります[ *DxgkDdiUpdateActiveVidPnPresentPath* ](https://msdn.microsoft.com/library/windows/hardware/ff560803)を設定して、 [ **DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062)構造体の**SupportSmoothRotation**メンバーは、Windows 8 以降で使用されます。
ドライバーを呼び出し中にパスの回転を設定することが常にある必要があります[ *DxgkDdiCommitVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559597)します。

## <a name="span-idsmoothrotationscenariosspanspan-idsmoothrotationscenariosspanspan-idsmoothrotationscenariosspansmooth-rotation-scenarios"></a><span id="Smooth_rotation_scenarios"></span><span id="smooth_rotation_scenarios"></span><span id="SMOOTH_ROTATION_SCENARIOS"></span>滑らかな回転シナリオ


従来のデスクトップおよびラップトップのシステムで画面の回転は頻繁に使用されるシナリオではありません。 モバイル デバイスでは多くの場合、主流のシナリオに画面の回転。 Windows 8 では、画面の回転時に、同期の監視が有効なままことを確認するための表示インフラストラクチャの最適化を使用します。 次の条件に該当する場合、滑らかな回転遷移をエンドユーザーことができます。

-   プラットフォームは、WDDM 1.2 を実行しています。
-   デスクトップ コンポジション manager では、上し、構成がアクティブにします。
-   モードの変更要求は、滑らかな回転モードへの移行に対応するように決定されます。 2 つのモードは、同じディメンション (幅と高さ) トポロジ レート、ピクセル形式、およびストライドを更新し、画面の向きだけが異なるがある場合は、互換性のある (つまり、回転) します。

 

 





