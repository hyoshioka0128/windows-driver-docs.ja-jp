---
title: 手順 2 のデバイスのドライバーが選択されています。
description: 手順 2 のデバイスのドライバーが選択されています。
ms.assetid: 2134cab6-58ea-4258-9a45-09bf54156e0a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e00a50a7836c30a7b4a86359c8603664ad9162e
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65456425"
---
# <a name="step-2-a-driver-for-the-device-is-selected"></a>手順 2:デバイスのドライバーが選択されます


新しいデバイスが検出され、Windows を識別した後、その[デバイス インストールのコンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff541277)これらの手順に従います。

1.  適切な Windows 検索[ドライバー パッケージ](driver-packages.md)デバイス。 この手順の詳細については、次を参照してください。[ドライバー パッケージを探して](#searching-for-the-driver)します。
2.  Windows では、1 つまたは複数のドライバー パッケージからデバイスの最適なドライバーを選択します。 この手順の詳細については、次を参照してください。 [、ドライバーを選択する](#selecting-the-driver)します。

### <a href="" id="searching-for-the-driver"></a>ドライバー パッケージの検索

使用して、[ハードウェア識別子 (ID)](hardware-ids.md)バスまたはハブのドライバー、Windows 検索によって報告された[ドライバー パッケージ](driver-packages.md)デバイスに一致します。 ハードウェア ID には、ハードウェア ID が一致する場合、ドライバー パッケージにデバイスと一致するか、[互換性 ID](compatible-ids.md)で、 [ **INF*モデル*セクション**](inf-models-section.md)のエントリドライバー パッケージの[INF ファイル](overview-of-inf-files.md)します。

オペレーティング システムのバージョンによっては、Windows は、次の表に示すようにさまざまな場所にドライバー パッケージに一致するを検索します。

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

 

たとえば、ユーザーには、Windows 7 を実行しているコンピューターに USB ハブのポートにワイヤレス ローカル エリア ネットワーク (WLAN) アダプターが接続されるため、次の手順が発生します。

-   USB ハブのドライバーが WLAN アダプターのハードウェア Id のリストを作成した後、Windows は最初に検索、[ドライバー ストア](driver-store.md)一致の[ドライバー パッケージ](driver-packages.md)デバイス。

-   デバイスのインストール プロセスは、次の場所のいずれかから一致するドライバー パッケージを検索します。

    -   汎用名前付け規則 (*UNC*) によって識別されるパス、 **DevicePath**のレジストリ値**HKEY_LOCAL_MACHINE\\ソフトウェア\\Microsoft\\Windows\\CurrentVersion**します。

    -   Windows Update

    -   デバイスの独立系ハードウェア ベンダー (IHV) が提供される、配布メディア。

    ドライバー パッケージが見つかった場合、Windows は、デバイスのドライバーのインストール元のドライバー ストアにパッケージをステージングします。

**注**  以降 Windows Vista では、オペレーティング システムはその常にインストール、[ドライバー パッケージ](driver-packages.md)から、[ドライバー ストア](driver-store.md)します。 一致するドライバー パッケージが別の場所にドライバー パッケージを格納、デバイスのドライバーのインストール前に、Windows の最初の段階で検出されます。

 

別の例として、ユーザーは、Windows 8 を実行しているコンピューターに USB ハブのポートに WLAN アダプターを接続されている場合は、次の手順が発生します。

-   USB ハブのドライバーには、WLAN アダプターのハードウェア ID が作成されたら、Windows が一致するドライバー ストアをまず[ドライバー パッケージ](driver-packages.md)デバイス。 ドライバー ストアにドライバー パッケージが見つかると、デバイスの Windows インストールします。 これにより、すばやく作業を開始するデバイスです。

-   別のプロセスで Windows Windows Update と検索をより適切に一致するドライバーの DevicePath がインストールされているよりもされます。 見つかった場合、ドライバーは、ドライバー ストアにステージングし、デバイス上にインストールされます。

詳細については、[ドライバー パッケージ](driver-packages.md)プロセスを検索しを参照してください[ドライバーが Windows 検索](where-setup-searches-for-drivers.md)します。

### <a name="selecting-the-driver"></a>ドライバーの選択

Windows の 1 つまたは複数の一致が見つかるとすぐに[ドライバー パッケージ](driver-packages.md)Windows デバイスの次の手順に従って、最適なドライバーを選択します。

1.  Windows が 1 つだけの一致するドライバー パッケージが見つかった場合、デバイスのパッケージからドライバーをインストールします。

2.  Windows が複数の一致するドライバー パッケージが見つかった場合 Windows 最初順位値に割り当てます、ドライバーからドライバー パッケージごと。 1 つのドライバーは、最も低い順位値がある、専用の場合は、そのパッケージのデバイスから、ドライバーがインストールされます。

    順位付けのプロセスの詳細については、次を参照してください。[ランク ドライバーをどのように Windows](how-setup-ranks-drivers.md)します。

3.  複数のドライバーには、同じの最も低い順位値がある、Windows は、次の条件を使用して、デバイスの最適なドライバーを選択します。

    -   ドライバーはデジタル署名するかどうか。 Windows Vista 以降、Windows は常に、他の選択条件に関係なく未署名のドライバーではなく、署名されたドライバーを選択します。 ドライバーのデジタル署名の詳細については、次を参照してください。[ドライバーの署名](driver-signing.md)します。

    -   ドライバーの日付と日付とバージョンがで指定されているバージョン、 [ **INF DriverVer ディレクティブ**](inf-driverver-directive.md)に含まれるドライバー パッケージの[INF ファイル](overview-of-inf-files.md)します。

」の説明に従って、Windows でドライバーをインストール後、Windows がデバイスのドライバーを選択すると、[手順 3。デバイスのドライバーがインストールされている](step-3--the-driver-for-the-device-is-installed.md)します。

デバイスのドライバーを選択する方法の詳細については、次を参照してください。 [Windows ドライバーを選択する方法](how-setup-selects-drivers.md)します。

 

 





