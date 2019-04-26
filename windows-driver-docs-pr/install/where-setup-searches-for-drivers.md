---
title: Windows のドライバーの検索場所
description: Windows のドライバーの検索場所
ms.assetid: 4c193b97-7b70-425f-99f2-ba976a4cc40a
keywords:
- ドライバーの選択、WDK のデバイスのインストール、デバイス setupsearches
- デバイス インストール WDK デバイスのインストール用のドライバーを検索する場所デバイス setupsearches
- デバイス インストール WDK デバイスのインストール中にドライバーを探しているデバイス setupsearches
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08daf6511d424e5d892c4c1afd13ff3f0db73b01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339303"
---
# <a name="where-windows-searches-for-drivers"></a>Windows のドライバーの検索場所


Windows が一致を検索しようとした、デバイスが接続されると、[ドライバー パッケージ](driver-packages.md)そこから、デバイスのドライバーをインストールできます。 Windows では、さまざまな場所からドライバー パッケージを検索し、次の表に示すように、2 段階でこの検索を実行します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">検索フェーズ</th>
<th align="left">Windows 7</th>
<th align="left">Windows 8 および Windows の以降のバージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ドライバーをインストールする前に</td>
<td align="left"><p>DevicePath</p>
<p>Windows Update</p>
<p><a href="driver-store.md" data-raw-source="[Driver store](driver-store.md)">ドライバー ストア</a></p></td>
<td align="left"><a href="driver-store.md" data-raw-source="[Driver store](driver-store.md)">ドライバー ストア</a></td>
</tr>
<tr class="even">
<td align="left">初期のドライバーを選択します。</td>
<td align="left"><p>適用なし</p></td>
<td align="left"><p>DevicePath</p>
<p>Windows Update</p></td>
</tr>
</tbody>
</table>

 

### <a name="searching-for-driver-packages"></a>ドライバー パッケージを検索

デバイスが接続されると、Windows は、最初に見つけて次のように、ユーザーの介入なしの信頼済みのシステム コンテキストでドライバーをインストールする回数します。

-   ドライバー ストアに既に存在する、最も一致するドライバーは最初に、操作をすばやく開始するデバイスを許可するデバイス上にインストールします。 並列および別のプロセスでは、次のように行われます。

-   Windows が自動的に一致するダウンロード[ドライバー パッケージ](driver-packages.md)Windows Update から。 Windows がパッケージをダウンロードし、段階的に一致するドライバー パッケージが見つかった場合、[ドライバー ストア](driver-store.md)します。 Windows 10 バージョン 1709 以降では、Windows で利用できる、最適なランク付けされたドライバーは必ずしも最新です。 ドライバーのランク付け考慮 HWID、日付/バージョン、および重要な/自動/省略可能なカテゴリ。 Windows には、最も高い重大または自動のドライバーが順位付けされます。 一致するドライバーが見つからない場合 WU は省略可能なドライバーの [次へ] を検索します。 その結果、それ以外の場合と同じランクの以前の不可欠なドライバーは、新しいオプションのドライバーに優先します。 Windows バージョン 1709 より前 Windows で利用できる重要で省略可能な更新プログラムと同じ優先順位。

    Windows で指定されている場所に事前に読み込まれていたするドライバー パッケージも検索、 **DevicePath**レジストリ値。 この値は、次のレジストリのサブキーの下でです。

    ```cpp
    HKEY_LOCAL_MACHINE
       Software
          Microsoft
             Windows
                CurrentVersion
    ```

    既定で、 **DevicePath**値の指定、%systemroot%\\INF ディレクトリ。

    Windows Update でまたはが指定されている場所のいずれかが最初にインストールされているドライバー パッケージが見つからないより一致する場合は、 **DevicePath**値では、Windows を最初にステージングするドライバー パッケージ、[ドライバー ストア](driver-store.md)ドライバーをインストールする前にします。 これにより、Windows は常に、ドライバー ストアからドライバーをインストールします。

 

 





