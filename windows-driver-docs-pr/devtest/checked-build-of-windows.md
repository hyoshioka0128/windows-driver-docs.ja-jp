---
title: Windows のチェック ビルド
description: Windows のチェック ビルド
ms.assetid: c0e5ccc4-78fc-4c48-a6d7-2f9825aa7de2
keywords:
- 検証 (WDK)、チェックされたビルド
- ドライバー検証 WDK、チェックされたビルド
- チェック済みビルドの WDK
- デバッグビルドの WDK
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4c7caa16c497f8826c37100bdf8a8e2564c55295
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999071"
---
# <a name="checked-build-of-windows"></a>Windows のチェック ビルド

## <span id="ddk_using_the_checked_build_of_windows_tools"></span><span id="DDK_USING_THE_CHECKED_BUILD_OF_WINDOWS_TOOLS"></span>

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

このセクションでは、Windows オペレーティングシステムの Microsoft Windows*チェックビルド*(*デバッグビルド*とも呼ばれます) が、このオペレーティングシステムの*無料ビルド*(*リテールビルド*とも呼ばれます) と異なる方法について説明します。 このセクションでは、x86 および x64 プラットフォームでのドライバーの開発とデバッグに、チェックされたビルドの固有の機能がどのように役立つかについて説明します。 また、さまざまなドライバーの開発およびデバッグ環境でチェックされたビルドをインストールおよび使用するためのいくつかの方法についても説明します。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容

-   [チェック ビルドと無料ビルドの違い](checked-and-free-build-differences.md)
-   [Windows のチェック ビルドの使用](using-the-checked-build.md)
-   [Windows のチェック ビルドのインストール](installing-the-checked-build.md)
-   [チェック ビルドのブレークポイントとメッセージ](checked-build-breakpoints-and-messages.md)
-   [チェック ビルドの ASSERT](checked-build-asserts.md)
