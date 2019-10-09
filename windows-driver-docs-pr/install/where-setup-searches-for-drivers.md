---
title: Windows のドライバーの検索場所
description: Windows のドライバーの検索場所
ms.assetid: 4c193b97-7b70-425f-99f2-ba976a4cc40a
keywords:
- ドライバー選択の WDK デバイスのインストール、デバイスの setupsearches
- デバイスのインストールに使用する WDK デバイスのドライバーの特定デバイスの setupsearches
- デバイスのインストール中にドライバーを検索する WDK デバイスのインストール (デバイスの setupsearches)
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 861a2fea00fcc7f7cb5ecf1cc17805f86d86ff7b
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007647"
---
# <a name="where-windows-searches-for-drivers"></a>Windows のドライバーの検索場所


デバイスが接続されると、Windows は、デバイスのドライバーをインストールできる、一致する[ドライバーパッケージ](driver-packages.md)の検索を試みます。 Windows は、次の表に示すように、さまざまな場所からドライバーパッケージを検索し、2つのフェーズでこの検索を実行します。

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

 

### <a name="searching-for-driver-packages"></a>ドライバーパッケージを検索しています

デバイスが接続されると、Windows はまず、次のように、ユーザーの介入なしに、信頼されたシステムコンテキストでドライバーの検索とインストールを試みます。

-   ドライバーストアに既に存在する最適なドライバーは、デバイスに最初にインストールされます。これにより、デバイスはすぐに操作を開始できます。 並列で、および別のプロセスでは、次の処理が行われます。

-   Windows は、一致する[ドライバーパッケージ](driver-packages.md)を Windows Update から自動的にダウンロードします。 一致するドライバーパッケージが見つかった場合は、Windows によってパッケージがダウンロードされ、[ドライバーストア](driver-store.md)にステージングされます。 Windows 10 バージョン1709以降では、Windows で最も優先順位の高いドライバーが提供されていますが、これは必ずしも最新ではありません。 ドライバーのランク付けでは、HWID、日付/バージョン、および重大/自動/オプションのカテゴリが考慮されます。 Windows では、重要なドライバーまたは自動ドライバーの優先順位が高くなります。 一致するドライバーが見つからない場合、WU は次にオプションのドライバーを検索します。 その結果、より優先順位の低い古い重要なドライバーが、新しいオプションのドライバーよりも優先されます。 1709より前の Windows バージョンでは、Windows では重要な更新プログラムとオプションの更新プログラムが提供され、優先順位は等しくなります。

    また、 **DevicePath**レジストリ値によって指定された場所にプリロードされたドライバーパッケージを検索します。 この値は、レジストリの次のサブキーの下にあります。

    ```cpp
    HKEY_LOCAL_MACHINE
       Software
          Microsoft
             Windows
                CurrentVersion
    ```

    既定では、 **DevicePath**値は% SystemRoot% \\inf ディレクトリを指定します。

    Windows Update または**DevicePath**値で指定された場所に、最初にインストールされたよりも適切なドライバーパッケージが見つかった場合、Windows は、ドライバーパッケージをドライバー[ストア](driver-store.md)にステージングしてから、ドライバーがら. このようにして、Windows は常にドライバーストアからドライバーをインストールします。

 

 





