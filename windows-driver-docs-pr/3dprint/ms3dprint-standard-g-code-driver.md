---
title: MS3DPrint 標準 G コード ドライバー
description: MS3DPrint G コードの標準的なドライバーが融合型・ フィラメント ・製造 3D プリンター用に G コードを実行し、特に RepRap プロジェクトのものを含むソースのプリンターを開き、一般的な Windows 8.1 または Windows 10 ドライバーを実装します。
ms.assetid: F5818F58-C705-458F-9806-3F840BF7EE01
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa433689f8ccd56b7a494a019655a3995798a72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324760"
---
# <a name="ms3dprint-standard-g-code-driver"></a>MS3DPrint 標準 G コード ドライバー


MS3DPrint G コードの標準的なドライバーは、汎用の Windows 8.1 または融合型・ フィラメント ・製造 3D プリンター用に G コードを実行し、特に RepRap プロジェクトから派生したものも含め、ソースのプリンターを開き、以降のバージョンのドライバーを実装します。

このドライバー セットには、ワイヤ プロトコルを実装する USB ドライバーとツールパスにジオメトリを変換するスライサーの両方が含まれています。 スライサーのドライバーでは、Windows スプーラーから 3MF データを受信し、USB ドライバーの G コードを出力します。 USB ドライバーは、シリアル接続経由で、一度に 1 つの G コード命令を送信します。 

USB ドライバーと、スライサーの両方、アクティブな開発され、実装と仕様の部分は、将来のリビジョンで変更されることはできます。  これらのドライバーのセットが Windows Update に公開されたし、サポートされているデバイスまたは MS_COMP_3DPRINT USB 記述子を使用して 3D プリンター自体を宣言するデバイスが自動的に提供します。
 

## <a name="3d-printing-sdk-driver-folder-contents"></a>3D 印刷 SDK ドライバー フォルダーの内容


次の表は、ドライバー、スライサーの位置に関する情報を提供し、3D 印刷 SDK でのフィルターを表示します。

| Folder                    | 目次                                 |
|---------------------------|------------------------------------------|
| \\Bin                     | コンパイルされたバイナリ                        |
| \\Bin\\MS3DPrintUSB\_x64  | ドライバー パッケージの 64 ビットの USB シリアル ポート    |
| \\Bin\\MS3DPrintUSB\_x86  | ドライバー パッケージを 32 ビットの USB シリアル ポート    |
| \\Bin\\RenderFiltersV4\_x64 | 64 ビットのスライサーおよびフィルター パッケージのレンダリング |
| \\Bin\\RenderFiltersV4\_x86 | 64 ビットのスライサーおよびフィルター パッケージのレンダリング |

 

## <a name="in-this-section"></a>このセクションの内容


[ドライバーのインストール](driver-installation.md)

[デバイスを構成します。](configuring-the-device.md)

[スライサーの設定](slicer-settings.md)

[XML のサンプル構成](sample-configuration-xml.md)

 




