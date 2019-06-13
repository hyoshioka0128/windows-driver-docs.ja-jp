---
title: コンピューター ハードウェア ID (CHID) の使用
description: コンピューター ハードウェア ID (CHID) の定義については、コンピューターのハードウェア ID の指定に関するページをご覧ください。
ms.assetid: 45DCAED5-8D20-4A31-B316-0460AB030DAD
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44b223e99c2be3f0efeeed7360e0620c35d0462f
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63334879"
---
# <a name="using-computer-hardware-ids-chids"></a>コンピューター ハードウェア ID (CHID) の使用


コンピューター ハードウェア ID (CHID) の定義については、[コンピューターのハードウェア ID の指定に関するページ](https://msdn.microsoft.com/windows/hardware/drivers/install/specifying-hardware-ids-for-a-computer)をご覧ください。

Windows 10 では、ベースボード製造元とベースボード製品情報を組み込んだいくつかの新しい CHID が追加されています。 次の表に示すように、これらの新しい CHID は CHID 階層に含まれています。 次の表では、限定性の高い順に階層を示しています。 Windows 10 で新しく追加された CHID は、はっきりわかるように太字で示されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>HWID</th>
<th>目次</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HardwareID-0</p></td>
<td><p>製造元 + ファミリ + 製品名 + SKU 番号 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース</p></td>
</tr>
<tr class="even">
<td><p>HardwareID-1</p></td>
<td><p>製造元 + ファミリ + 製品名 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-2</p></td>
<td><p>製造元 + 製品名 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース</p></td>
</tr>
<tr class="even">
<td><p>HardwareID-3</p></td>
<td><p><strong>製造元 + ファミリ + 製品名 + SKU 番号 + ベースボード製造元 + ベースボード製品</strong></p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-4</p></td>
<td><p>製造元 + ファミリ + 製品名 + SKU 番号</p></td>
</tr>
<tr class="even">
<td><p>HardwareID-5</p></td>
<td><p>製造元 + ファミリ + 製品名</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-6</p></td>
<td><p><strong>製造元 + SKU 番号 + ベースボード製造元 + ベースボード製品</strong></p></td>
</tr>
<tr class="even">
<td><p>HardwareID-7</p></td>
<td><p>製造元 + SKU 番号</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-8</p></td>
<td><p><strong>製造元 + 製品名 + ベースボード製造元 + ベースボード製品</strong></p></td>
</tr>
<tr class="even">
<td><p>HardwareID-9</p></td>
<td><p>製造元 + 製品名</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-10</p></td>
<td><p><strong>製造元 + ファミリ + ベースボード製造元 + ベースボード製品</strong></p></td>
</tr>
<tr class="even">
<td><p>HardwareID-11</p></td>
<td><p>製造元 + ファミリ</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-12</p></td>
<td><p>製造元 + 筐体の種類</p></td>
</tr>
<tr class="even">
<td><p>HardwareID-13</p></td>
<td><p><strong>製造元 + ベースボード製造元 + ベースボード製品</strong></p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-14</p></td>
<td><p>製造元</p></td>
</tr>
</tbody>
</table>

 

OEM は、ドライバーの発行者に正しい CHID 情報を提供する必要があります。 Windows Desktop Tools SDK に含まれている [ComputerHardwareIds](https://msdn.microsoft.com/library/windows/hardware/ff543505) ツールは、既知の System Management BIOS (SMBIOS) の値のセットから CHID を報告するのに役立ちます。 ComputerHardwareIds は 2 種類のタスクを実行します。

1.  既定の動作:ツールでは、システムの SMBIOS 値と生成された CHID が報告されます。

    既定では、ツールは、システムの SMBIOS 値、および SMBIOS 値から生成された CHID を表示します。

2.  シミュレーションの動作: ツールでは、ユーザーが指定した SMBIOS 値から CHID が生成されます。

    シミュレートされた SMBIOS 値 (製造元、ファミリ、SKU など) を指定してツールを実行することにより、生成された CHID のリストを取得できます。 これにより、特定の SMBIOS データ値を持つシステムで生成される CHID を確認できます。

## <a name="span-idtipsforconsistentchidsspanspan-idtipsforconsistentchidsspanspan-idtipsforconsistentchidsspantips-for-consistent-chids"></a><span id="Tips_for_consistent_CHIDs"></span><span id="tips_for_consistent_chids"></span><span id="TIPS_FOR_CONSISTENT_CHIDS"></span>一貫性のある CHID のためのヒント


CHID は、大文字と小文字を区別した SMBIOS 値に基づいて生成されます。 システムで、SMBIOS テキスト値で大文字と小文字が混在しないように注意する必要があります。 同様に、UNICODE 文字は特別に扱われません。 大文字と小文字のバージョンの特殊文字 (トルコ語のドット付きとドットなしの I など) は一意に処理されます。I、ı、İ、および i は同じではありません。

ComputerHardwareIds ツールは、必要な SMBIOS 値が利用可能である場合にのみ CHID を計算します。 SMBIOS データ フィールドが見つからない (または null である) 場合は、関連する CHID は生成されません。 たとえば、SMBIOS の SKU フィールドが null の場合、その特定のシステムでは、CHID 0、3、4、6、7 は使用できません。

CHID について詳しくは、「[Specifying Hardware IDs for a Computer (コンピューターのハードウェア ID の指定)](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer)」をご覧ください。

 

 





