---
title: サービス アイコンの要件
description: サービス アイコンの要件
ms.assetid: ce018a26-f5ce-4fbb-8339-b3207ca5ed68
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d01802185f3436773f419af5435f8c51452c079
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518584"
---
# <a name="service-icon-requirements"></a>サービス アイコンの要件


サービス アイコンは、Windows 接続マネージャーで移動体通信事業者 (MNO) や仮想移動体通信事業者 (MVNO) のロゴを表示するために使われます。

このファイルは、次の要件のいずれかを満たす .ICO ファイルである必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>256x256: 32 ビット + アルファ (圧縮)</p></td>
<td><p>24x24: 32 ビット + アルファ</p></td>
</tr>
<tr class="even">
<td><p>48 ｘ 48: 32 ビット + アルファ</p></td>
<td><p>24 ｘ 24: 8 ビット 256 色</p></td>
</tr>
<tr class="odd">
<td><p>48 ｘ 48: 8 ビット 256 色</p></td>
<td><p>24 ｘ 24: 4 ビット 16 色</p></td>
</tr>
<tr class="even">
<td><p>48 ｘ 48: 4 ビット 16 色</p></td>
<td><p>16 ｘ 16: 32 ビット + アルファ</p></td>
</tr>
<tr class="odd">
<td><p>32 ｘ 32: 32 ビット + アルファ</p></td>
<td><p>16x16: 8 ビット 256 色</p></td>
</tr>
<tr class="even">
<td><p>32x32: 8 ビット 256 色</p></td>
<td><p>16x16: 4 ビット 16 色</p></td>
</tr>
<tr class="odd">
<td><p>32x32: 4 ビット 16 色</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

 

サービス アイコンは、サービス メタデータ パッケージの [ServiceInfo XML スキーマ](https://msdn.microsoft.com/library/windows/hardware/dn973167)の [ServiceIconFile](https://msdn.microsoft.com/library/windows/hardware/dn973162) 要素に関連付けられます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

- [モバイル ブロードバンド エクスペリエンスの作成](https://msdn.microsoft.com/library/windows/hardware/dn236414.aspx)

 

 






