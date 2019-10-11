---
title: Windows 8 の Direct3D ハードウェア要件
description: このトピックでは、Windows 8 で Microsoft Direct3D をサポートするためのハードウェア要件について説明します。
ms.assetid: 7297C938-D2DD-4A06-B9AD-18DDAA73A1E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da62c6ee2bc4e872794cdf16480b408381037974
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038102"
---
# <a name="direct3d-hardware-requirements-in-windows-8"></a>Windows 8 の Direct3D ハードウェア要件


このトピックでは、Windows 8 で Microsoft Direct3D をサポートするためのハードウェア要件について説明します。

独立系ハードウェアベンダーは、この表で指定されているハードウェアの Windows 8 Direct3D レンダリング要件に従う必要があります。 詳細については、「 [Windows 8 での DirectX の機能強化](directx-feature-improvements-in-windows-8.md)」も参照してください。

**ハードウェアの Direct3D レンダリング要件**

| Microsoft DirectX ハードウェアのバージョン | 必須/オプション | Windows 8 のレンダリング要件 |
|------------------------------------|-------------------|----------------------------------|
| D3D9                               | 必須          | D3D9 HW 仕様                     |
| D3D10                              | 必須          | D3D9 HW 仕様                     |
| D3D10                              | 必須          | D3D10 HW 仕様                    |
| D3D 10.1                            | 必須          | D3D9 HW 仕様                     |
| D3D 10.1                            | 必須          | D3D10 HW 仕様                    |
| D3D 10.1                            | 必須          | D3D 10.1 HW 仕様                  |
| D3D11                              | 必須          | D3D9 HW 仕様                     |
| D3D11                              | 必須          | D3D10 HW 仕様                    |
| D3D11                              | 必須          | D3D 10.1 HW 仕様                  |
| D3D11                              | 必須          | D3D11 HW 仕様                    |
| D3D 11.1                            | 必須          | D3D9 HW 仕様                     |
| D3D 11.1                            | 必須          | D3D10 HW 仕様                    |
| D3D 11.1                            | 必須          | D3D 10.1 HW 仕様                  |
| D3D 11.1                            | 必須          | D3D11 HW 仕様                    |
| D3D 11.1                            | 必須          | D3D 11.1 HW 仕様                  |

 

次の表では、Windows 8 の Direct3D ハードウェア仕様の更新について説明します。

**Windows 8 の Microsoft Direct3D 10 ハードウェア仕様の変更**

| 必須/省略可能      | 機能                            |
|----------------|------------------------------------|
| 必須       | ピクセル形式 (5551、565、4444) \* |
| 必須       | 同じ surface blits \*              |
| 実装されている場合 | Logic ops                          |

 

**Windows 8 の Direct3D 10.1 ハードウェア仕様の変更**

| 必須/省略可能      | 機能                            |
|----------------|------------------------------------|
| 必須       | ピクセル形式 (5551、565、4444) \* |
| 必須       | 同じ surface blits \*              |
| 実装されている場合 | Logic ops                          |

 

**Windows 8 の Microsoft Direct3D 11 ハードウェア仕様の変更**

| 必須/省略可能      | 機能                            |
|----------------|------------------------------------|
| 必須       | ピクセル形式 (5551、565、4444) \* |
| 必須       | 同じ surface blits \*              |
| 実装されている場合 | UAV-MSAA                           |
| 実装されている場合 | スレッドの同時作成       |
| 実装されている場合 | スレッドコマンド一覧            |
| 実装されている場合 | 倍精度のサポート           |
| 実装されている場合 | Logic ops                          |

 

**Windows 8 用 Direct3D 11.1 ハードウェア仕様**

| 必須/省略可能      | 機能                                |
|----------------|----------------------------------------|
| 必須       | Logic ops                              |
| 必須       | ピクセル形式 (5551、565、4444) \*     |
| 必須       | 同じ surface blits \*                  |
| 必須       | すべてのステージでの UAVs                    |
| 必須       | UAV-MSAA                               |
| 必須       | ターゲットに依存しないラスター化 (TIR) |
| 実装されている場合 | スレッドの同時作成           |
| 実装されている場合 | スレッドコマンド一覧                |
| 実装されている場合 | 倍精度のサポート               |

**\*** は既に Microsoft Direct3D 9 ハードウェア仕様に存在していますが、以前は Direct3D 10 で公開されていません。
