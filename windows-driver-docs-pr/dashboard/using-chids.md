---
title: コンピューター ハードウェア ID (CHID) の使用
description: コンピューター ハードウェア ID (CHID) の定義については、コンピューターのハードウェア ID の指定に関するページをご覧ください。
ms.assetid: 45DCAED5-8D20-4A31-B316-0460AB030DAD
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad7467b621ce12ca4429506be87f9a30c763b56
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "68483068"
---
# <a name="using-computer-hardware-ids-chids"></a>コンピューター ハードウェア ID (CHID) の使用


コンピューター ハードウェア ID (CHID) の定義については、[コンピューターのハードウェア ID の指定に関するページ](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer)をご覧ください。

Windows 10 では、ベースボード製造元とベースボード製品情報を組み込んだいくつかの新しい CHID が追加されています。 次の表に示すように、これらの新しい CHID は CHID 階層に含まれています。 次の表では、限定性の高い順に階層を示しています。 Windows 10 で新しく追加された CHID は、はっきりわかるように太字で示されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>HWID</th>
<th>内容</th>
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

 

OEM は、ドライバーの発行者に正しい CHID 情報を提供する必要があります。 Windows Desktop Tools SDK に含まれている [ComputerHardwareIds](https://docs.microsoft.com/windows-hardware/drivers/devtest/computerhardwareids) ツールは、既知の System Management BIOS (SMBIOS) の値のセットから CHID を報告するのに役立ちます。 ComputerHardwareIds は 2 種類のタスクを実行します。

1.  既定の動作:ツールでは、システムの SMBIOS 値と生成された CHID が報告されます。

    既定では、ツールは、システムの SMBIOS 値、および SMBIOS 値から生成された CHID を表示します。

2.  シミュレーションの動作: ツールでは、ユーザーが指定した SMBIOS 値から CHID が生成されます。

    シミュレートされた SMBIOS 値 (製造元、ファミリ、SKU など) を指定してツールを実行することにより、生成された CHID のリストを取得できます。 これにより、特定の SMBIOS データ値を持つシステムで生成される CHID を確認できます。

## <a name="span-idtips_for_consistent_chidsspanspan-idtips_for_consistent_chidsspanspan-idtips_for_consistent_chidsspantips-for-consistent-chids"></a><span id="Tips_for_consistent_CHIDs"></span><span id="tips_for_consistent_chids"></span><span id="TIPS_FOR_CONSISTENT_CHIDS"></span>一貫性のある CHID のためのヒント


CHID は、大文字と小文字を区別した SMBIOS 値に基づいて生成されます。 システムで、SMBIOS テキスト値で大文字と小文字が混在しないように注意する必要があります。 同様に、UNICODE 文字は特別に扱われません。 大文字と小文字のバージョンの特殊文字 (トルコ語のドット付きとドットなしの I など) は一意に処理されます。I、ı、İ、および i は同じではありません。

ComputerHardwareIds ツールは、必要な SMBIOS 値が利用可能である場合にのみ CHID を計算します。 SMBIOS データ フィールドが見つからない (または null である) 場合は、関連する CHID は生成されません。 たとえば、SMBIOS の SKU フィールドが null の場合、その特定のシステムでは、CHID 0、3、4、6、7 は使用できません。

CHID について詳しくは、「[Specifying Hardware IDs for a Computer (コンピューターのハードウェア ID の指定)](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer)」をご覧ください。

 
## <a name="span-idhow_windows_update_uses_chidspanspan-idhow_windows_update_uses_chidspanspan-idhow_windows_update_uses_chidspanhow-the-windows-update-service-uses-chid"></a><span id="How_Windows_Update_uses_CHID"></span><span id="how_windows_update_uses_chid"></span><span id="HOW_WINDOWS_UPDATE_USES_CHID"></span>Windows Update サービスで CHID を使用する方法


Windows Update サービスでは、CHID を使用して "ドライバーが適用できるシステムの数を減らします"。  この削減は、PnP ランキングが行われる前に最初に行われる処理です。

Windows Update サービスでは、インストールされている Windows OS レベルに応じて CHID の処理方法が異なります。  

<table>
<colgroup>
<col width="40%" />
<col width="60%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows 10 のバージョン</th>
<th>Windows Update の動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1507 から 1703</p></td>
<td><p>Windows Update によって、各 CHID は CHID-0 から CHID-14 に順位付けされます (CHID-0 は CHID-14 よりも上位です)。</p></td>
</tr>
<tr class="even">
<td><p>1709 以降</p></td>
<td><p>CHID レベルは順位付けされません。 CHID-0 から CHID-14 の適用可能な CHID の対象となるすべてのドライバーは、グループ化されてから、グループ全体に対して PnP の順位付けが行われます。</p></td>
</tr> 
</tbody>
</table>


次に例を示します。


Contoso は、同じ HWID をターゲットとして CHID が異なる次の 2 つのドライバーを自動として公開しています。  

    Distribution 1 - targeting CHID-4 (Manufacturer + Family + Product Name + SKU Number)

    Distribution 2 - targeting CHID-5 (Manufacturer + Family + Product Name)

CHID-5 に一致するシステムの Windows Update サービスによって選択されるのはどちらでしょうか。

<table>
<colgroup>
<col width="40%" />
<col width="30%" />
<col width="30%" />
</colgroup>
<thead>
<tr class="header">
<th>Contoso システム</th>
<th>Windows OS レベル</th>
<th>提供されるドライバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CHID-5 は一致しますが、CHID-4 は一致しません</p></td>
<td><p>Windows 10 1703 以前</p></td>
<td><p>ディストリビューション 2</p></td>
</tr>
<tr class="even">
<td><p>CHID-5 は一致しますが、CHID-4 は一致しません</p></td>
<td><p>Windows 10 1709 以降</p></td>
<td><p>ディストリビューション 2</p></td>
</tr>
<tr class="odd">
<td><p>CHID-5 が一致し、<strong>かつ</strong> CHID-4 が一致します</p></td>
<td><p>Windows 10 1703 以前</p></td>
<td><p>ディストリビューション 1</p></td>
</tr>
<tr class="even">
<td><p>CHID-5 が一致し、<strong>かつ</strong> CHID-4 が一致します</p></td>
<td><p>Windows 10 1709 以降</p></td>
<td><p>両方が提供されます。   PnP の順位付けによって、これら 2 つのインストールに最適な一致が選択されます。</p></td>
</tr>
</tbody>
</table>
 





