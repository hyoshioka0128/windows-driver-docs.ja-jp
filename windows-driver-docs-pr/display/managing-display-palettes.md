---
title: ディスプレイ パレットの管理
description: ディスプレイ パレットの管理
ms.assetid: a0ff1a9c-82dc-4317-a0ec-c387027a52ba
keywords:
- ディスプレイドライバー WDK Windows 2000、パレット
- カラー参照テーブル WDK Windows 2000 ディスプレイ
- パレット WDK Windows 2000 ディスプレイ
- カラーパレット WDK Windows 2000 ディスプレイ
- カラーインデックス WDK Windows 2000 ディスプレイ
- 設定可能なパレット WDK Windows 2000 ディスプレイ
- インデックス付きパレット WDK Windows 2000 ディスプレイ
- RGB 色 WDK Windows 2000 ディスプレイ
ms.date: 10/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: 891da21421057fb50e80eac3391bd1a55f2239d3
ms.sourcegitcommit: b7ba0d42117f30125ae2dcd4dcb16dd988a18ff3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72283737"
---
# <a name="managing-display-palettes"></a>ディスプレイ パレットの管理

設定可能な色がビデオハードウェアでサポートされている場合は、*パレット*と呼ばれるカラールックアップテーブルが保持されます。 GDI は、各 RGB 値を取得し、それをデバイスの*カラーインデックス*に変換して表示できるようにします。 GDI は、事前に計算され、キャッシュされたテーブルを翻訳に使用します。 これらのテーブルは、ユーザーオブジェクトの[*Xlateobj*](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-xlateobj)としてドライバーにアクセスできます。 したがって、ソースの色を取得して変換先のデバイスに移動するすべての GDI グラフィックス関数は、XLATEOBJ 構造体を使用して色を変換します。 パレットと GDI がそれらを処理する方法の詳細については、「 [gdi でのパレットのサポート](gdi-support-for-palettes.md)」を参照してください。

ビデオハードウェアで設定できるパレットがサポートされている場合、GDI は、アプリケーションによって要求された[**DrvSetPalette**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvsetpalette)を呼び出します。 GDI は新しいパレットをディスプレイドライバーに渡し、ドライバーは[、その新しい](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-palobj)パレットを作成します。

**DrvSetPalette**関数は、ドライバーへの*pdev*へのハンドルを提供し、そのデバイスのパレットを認識するようにドライバーに要求します。 ドライバーは、指定されたパレットのエントリとできるだけ一致するようにハードウェアパレットを設定する必要があります。

このエントリポイントは、デバイスが設定できるパレットをサポートしている場合に必要であり、それ以外の場合は指定しないでください。 ディスプレイドライバーは、Drno__t- **0FlGraphicsCaps**を設定することによって、そのデバイスに設定可能なパレットがあることを指定します。このビットは、 [**Dr**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)の[DEVINFO](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-devinfo)構造体のフィールドに設定します。

サービスルーチン[PALOBJ_cGetColors](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-palobj_cgetcolors)を使用して、ドライバーを表示できます。 この関数は、インデックス付きパレットから RGB 色をダウンロードし、 *DrvSetPalette*の実装内から呼び出す必要があります。
