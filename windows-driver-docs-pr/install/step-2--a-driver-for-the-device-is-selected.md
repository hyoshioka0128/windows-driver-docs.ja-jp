---
title: 手順 2. デバイスのドライバーが選択されている
description: 手順 2. デバイスのドライバーが選択されている
ms.assetid: 2134cab6-58ea-4258-9a45-09bf54156e0a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cce40c6cc81d3c3ad2664536cda736568a95c17b
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557787"
---
# <a name="step-2-a-driver-for-the-device-is-selected"></a>手順 2:デバイスのドライバーが選択されます


新しいデバイスが検出され、識別された後、Windows とその[デバイスのインストールコンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))は、次の手順に従います。

1.  Windows は、デバイスに適した[ドライバーパッケージ](driver-packages.md)を検索します。 このステップの詳細については、「[ドライバーパッケージの検索](#searching-for-the-driver)」を参照してください。
2.  Windows は、1つまたは複数のドライバーパッケージから、デバイスに最適なドライバーを選択します。 この手順の詳細については、「[ドライバーの選択](#selecting-the-driver)」を参照してください。

### <a name="searching-for-the-driver-package"></a><a href="" id="searching-for-the-driver"></a>ドライバーパッケージを検索しています

バスまたはハブドライバーによって報告された[ハードウェア識別子 (ID)](hardware-ids.md)を使用して、Windows は、デバイスに一致する[ドライバーパッケージ](driver-packages.md)を検索します。 ドライバーパッケージは、ドライバーパッケージの[inf ファイル](overview-of-inf-files.md)の " [**inf*モデル*" セクション**](inf-models-section.md)エントリのハードウェア ID または互換性のある[id](compatible-ids.md)と一致するハードウェア id である場合に、デバイスと一致します。

オペレーティングシステムのバージョンに応じて、Windows は次の表に示すように、さまざまな場所で一致するドライバーパッケージを検索します。

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
<th align="left">Windows 8 以降のバージョンの Windows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ドライバーがインストールされる前</td>
<td align="left"><p>DevicePath</p>
<p>Windows Update</p>
<p><a href="driver-store.md" data-raw-source="[Driver store](driver-store.md)">ドライバーストア</a></p></td>
<td align="left"><a href="driver-store.md" data-raw-source="[Driver store](driver-store.md)">ドライバーストア</a></td>
</tr>
<tr class="even">
<td align="left">最初のドライバーが選択された後</td>
<td align="left"><p>適用なし</p></td>
<td align="left"><p>DevicePath</p>
<p>Windows Update</p></td>
</tr>
</tbody>
</table>

 

たとえば、ユーザーが Windows 7 を実行しているコンピューター上のワイヤレスローカルエリアネットワーク (WLAN) アダプターを USB ハブのポートに接続している場合、次の手順が実行されます。

-   USB ハブドライバーは、WLAN アダプターのハードウェア Id の一覧を作成した後、[ドライバーストア](driver-store.md)でデバイス用の一致する[ドライバーパッケージ](driver-packages.md)を検索します。

-   デバイスのインストールプロセスでは、次のいずれかの場所から、一致するドライバーパッケージが検索されます。

    -   **HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ Windows \\ CurrentVersion**の**DevicePath**レジストリ値によって識別される汎用名前付け規則 (*UNC*) パス。

    -   Windows Update

    -   独立系ハードウェアベンダー (IHV) によってデバイスに提供された配布メディア。

    ドライバーパッケージが見つかった場合、Windows は、デバイスのドライバーをインストールするドライバーストアにパッケージをステージングします。

**メモ**   Windows Vista 以降では、オペレーティングシステムは常にドライバー[ストア](driver-store.md)から[ドライバーパッケージ](driver-packages.md)をインストールします。 一致するドライバーパッケージが別の場所に存在する場合、Windows はまず、デバイスのドライバーをインストールする前に、ドライバーストアにパッケージをステージングします。

 

別の例として、ユーザーが Windows 8 を実行しているコンピューター上の USB ハブのポートに WLAN アダプターを接続すると、次の手順が実行されます。

-   USB ハブドライバーが WLAN アダプターのハードウェア ID を作成した後、Windows はまず、ドライバーストアで、デバイスに対応する[ドライバーパッケージ](driver-packages.md)を検索します。 ドライバーパッケージがドライバーストアで見つかった場合は、Windows によってデバイスにインストールされます。 これにより、デバイスはすぐに作業を開始できます。

-   別のプロセスでは、Windows によって Windows Update が検索され、インストールされたドライバーよりも適切なドライバーが検出されます。 ドライバーが見つかった場合は、ドライバーがドライバーストアにステージングされ、デバイスにインストールされます。

[ドライバーパッケージ](driver-packages.md)の検索プロセスの詳細については、「 [Windows がドライバーを検索する場所](where-setup-searches-for-drivers.md)」を参照してください。

### <a name="selecting-the-driver"></a>ドライバーの選択

Windows によってデバイスに対応する[ドライバーパッケージ](driver-packages.md)が1つ以上検出されると、windows は、次の手順に従って最適なドライバーを選択します。

1.  一致するドライバーパッケージが1つだけ検出された場合は、そのパッケージからデバイス用のドライバーがインストールされます。

2.  一致するドライバーパッケージが複数検出された場合、Windows はまず、各ドライバーパッケージからドライバーに順位付け値を割り当てます。 順位値が最も低いドライバーが1つしかない場合は、そのパッケージからデバイス用のドライバーがインストールされます。

    順位付けプロセスの詳細については、「 [Windows がドライバーをランク付けする方法](how-setup-ranks-drivers--windows-vista-and-later-.md)」を参照してください。

3.  複数のドライバーの順位値が同じである場合、Windows は次の条件を使用してデバイスに最適なドライバーを選択します。

    -   ドライバーがデジタル署名されているかどうか。 Windows Vista 以降では、他の選択条件に関係なく、Windows は常に署名されたドライバーではなく署名されたドライバーを選択します。 ドライバーのデジタル署名の詳細については、「[ドライバーの署名](driver-signing.md)」を参照してください。

    -   ドライバーの日付とバージョン。日付とバージョンは、ドライバーパッケージの[inf ファイル](overview-of-inf-files.md)に格納されている[**inf DriverVer ディレクティブ**](inf-driverver-directive.md)によって指定されます。

Windows によってデバイスのドライバーが選択されると、「[手順 3: デバイスのドライバーがインストールさ](step-3--the-driver-for-the-device-is-installed.md)れている」の説明に従ってドライバーがインストールされます。

デバイスのドライバーを選択する方法の詳細については、「 [Windows がドライバーを選択する方法](how-setup-selects-drivers.md)」を参照してください。

 

 





