---
title: Windows 8 での Direct3D のソフトウェア要件
description: このトピックでは、Windows 8 でマイクロソフトの Direct3D をサポートするソフトウェアの要件について説明します。
ms.assetid: EB9AB15A-4E47-48AE-AE39-6051F8FC39A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50ad434b8d769ba7189b442ff67b1e06fd7b0d05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391216"
---
# <a name="direct3d-software-requirements-in-windows-8"></a>Windows 8 での Direct3D のソフトウェア要件


このトピックでは、Windows 8 でマイクロソフトの Direct3D をサポートするソフトウェアの要件について説明します。

Windows 8 では、独立系ハードウェア ベンダー書き込む必要があります、関連する Direct3D 機能レベルのユーザー モード ドライバーをサポートできる Windows Display Driver Model (WDDM) 1.2 ドライバー (UMD) のデバイス ドライバー インターフェイス (Ddi)。

たとえば、マイクロソフトの Direct3D 9 対応ハードウェアする必要があります、少なくとも、サポート、Direct3D のバージョン 9 DDI します。 これらのソフトウェア要件は異なる次の表で指定されている Microsoft DirectX ハードウェア レベルに基づいています。

**DirectX のソフトウェア要件**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectX ハードウェア</th>
<th align="left">ソフトウェア要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">D3D9</td>
<td align="left"><p>［必須］:WDDM 1.2</p>
<p>［必須］:D3D9 - UMD DDI</p></td>
</tr>
<tr class="even">
<td align="left">D3D10</td>
<td align="left"><p>［必須］:WDDM 1.2</p>
<p>［必須］:D3D9 - UMD DDI</p>
<p>［必須］:D3D10 UMD DDI</p>
<p>［必須］:D3D11.1 - UMD DDI</p></td>
</tr>
<tr class="odd">
<td align="left">D3D10.1</td>
<td align="left"><p>［必須］:WDDM 1.2</p>
<p>［必須］:D3D9 - UMD DDI</p>
<p>［必須］:D3D10 UMD DDI</p>
<p>［必須］:D3D10.1 UMD DDI</p>
<p>［必須］:D3D11.1 - UMD DDI</p></td>
</tr>
<tr class="even">
<td align="left">D3D11</td>
<td align="left"><p>［必須］:WDDM 1.2</p>
<p>［必須］:D3D9 - UMD DDI</p>
<p>［必須］:D3D10 UMD DDI</p>
<p>［必須］:D3D10.1 UMD DDI</p>
<p>［必須］:D3D11 - UMD DDI</p>
<p>［必須］:D3D11.1 - UMD DDI</p></td>
</tr>
<tr class="odd">
<td align="left">D3D11.1</td>
<td align="left"><p>［必須］:WDDM 1.2</p>
<p>［必須］:D3D9 - UMD DDI</p>
<p>［必須］:D3D10 UMD DDI</p>
<p>［必須］:D3D10.1 UMD DDI</p>
<p>［必須］:D3D11 - UMD DDI</p>
<p>［必須］:D3D11.1 - UMD DDI</p></td>
</tr>
</tbody>
</table>

 

次の表では、Windows 8 のユーザー モード ドライバー (UMD) DDI の変更を使用して、公開されている機能について説明します。

**D3D9 - UMD DDI は Windows 8 では、次の新機能を公開します。**

| 必須/省略可能 | 機能                  |
|-----------|--------------------------|
| 必須  | 上書きして破棄の欠如 |
| 必須  | Tileable コピー フラグ       |

 

**D3D11.1 - UMD DDI 10 や 10.1、11、11.1 の機能レベルで Windows 8 では次の新機能を公開します**

| 必須/省略可能      | 機能                                                                            |
|----------------|------------------------------------------------------------------------------------|
| 必須       | 上書きして破棄の欠如                                                           |
| 必須       | テクスチャの配列 (ステレオスコ ピック 3D を含む) のプロセス間を共有するためのサポート    |
| 必須       | Tileable コピー フラグ                                                                 |
| 必須       | ClearView                                                                          |
| 実装されている場合 | Ops のロジック                                                                          |
| 必須       | ピクセル形式 (5551、565、4444) の正確なサポートは、機能レベルによって異なります。        |
| 必須       | 同じ画面ブリット                                                                 |
| 必須       | 定数バッファーが部分的な更新プログラム                                                    |
| 必須       | オフセット定数バッファーのバインド                                                        |
| 必須       | 強化されたリソースの共有                                                          |
| 必須       | SampleCount = 1 (制限付きターゲットに依存しないラスタライズ (TIR) で 10 や 10.1、11) |

 

**D3D11.1 - UMD DDI は 11 & 11.1 の機能レベルの次の新機能を公開します。**

| 必須/省略可能      | 機能                                   |
|----------------|-------------------------------------------|
| 必須       | UAV MSAA                                  |
| 実装されている場合 | 倍精度シェーダー機能     |
| 必須       | 絶対誤差 (MSAD) のマスク合計 |

 

**D3D11.1 - UMD DDI は 11.1 の機能レベルの次の新機能を公開します。**

| 必須/省略可能 | 機能                  |
|-----------|--------------------------|
| 必須  | すべてのステージにおいて UAVs      |
| 必須  | UAV MSAA (で 16 のサンプル) |
| 必須  | TIR                      |

 

 

 





