---
title: CPSUI の概要
description: CPSUI の概要
ms.assetid: 737c2dbf-1ce6-4f83-af94-265c948f3128
keywords:
- 一般的なプロパティ シートのユーザー インターフェイス WDK CPSUI についての印刷
- CPSUI WDK CPSUI についての印刷
- WDK プロパティ シートのページを印刷するプリンター ドライバーで CPSUI について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69cd6fff7da2f4b3b8668b8e10199805a75e5dc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552810"
---
# <a name="introduction-to-cpsui"></a>CPSUI の概要





一般的なプロパティ シートのユーザー インターフェイス (CPSUI) は、開発者が共通の標準的な外観のプロパティ シート ページを作成することができるユーザー モードのダイナミック リンク ライブラリです。 CPSUI で作成されたほとんどのページが構成されます。

-   ページの選択可能なユーザーが変更可能なオプションを表す各ツリー ノードのツリー ビュー ウィンドウ。

-   表示して、ノードに関連付けられたパラメーターの値を選択するため、各ツリー ノードのコンテキスト メニュー。

定義済みのセットを使用してコンテキスト メニュー項目が作成された[CPSUI でサポートされているウィンドウ コントロール](cpsui-supported-window-controls.md)します。 ユーザーは、ツリー ビュー ウィンドウで、オプションを選択し、コンテキスト メニューを使用してそのオプションは、目的の値を選択します。

CPSUI は、任意のアプリケーションで使用するように設計、主な用途が NT ベースのオペレーティング システムの印刷サブシステムができます。 そのため、Windows Driver Kit (WDK) ドキュメントでは、このような使用について説明します。

CPSUI は、プリンターおよび印刷するドキュメントの定義済みのプロパティ シートのページを提供します。 CPSUI が指定したページから成る、**デバイス設定**、プリンターのページと**レイアウト**、**用紙/品質**と**詳細**ページドキュメント。 これらのページは、印刷フォルダーから表示できます**プリンター**メニュー。

組み合わせて、印刷スプーラー[プリンター インターフェイス Dll](printer-interface-dll.md)、これらの定義済みページを使用して、プリンターおよびドキュメントのプロパティ シートを作成します。 印刷スプーラー、プリンター インターフェイス Dll、および CPSUI がやり取りする方法については、次を参照してください。[プリンター ドライバーを使用して CPSUI](using-cpsui-with-printer-drivers.md)します。

Microsoft の用に作成されたユーザー インターフェイスのコードをカスタマイズ*Unidrv*と*Pscript*ドライバーが CPSUI を使用してもできます。 詳細については、次を参照してください。[ユーザー インターフェイスのプラグイン](user-interface-plug-ins.md)します。

 

 




