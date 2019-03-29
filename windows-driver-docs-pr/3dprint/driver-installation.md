---
title: ドライバーのインストール
description: この SDK で提供される、印刷ドライバーでは、まだ開発中の実験用の 3D プリンター デバイス ドライバーです。
ms.assetid: 8A13CD6F-DF82-4353-ADE9-06989F83BC87
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d6617e65e995a45353bb0a8aa178dbfa2f95607
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581934"
---
# <a name="driver-installation"></a>ドライバーのインストール


> [!NOTE]
> 3D 印刷 SDK で提供される、印刷ドライバーでは、まだ開発中の実験用の 3D プリンター デバイス ドライバーです。

## <a name="driver-installation"></a>ドライバーのインストール


プリンターをインストールするには、次のインストール手順を使用します。

- 3D プリンターが、Microsoft OS ディスクリプター 3DPRINT を実装するかどうか ("MS\_COMP\_3DPRINT") がサポートされている仕入先 ID (VID) のいずれかまたは製品 ID (PID) の組み合わせ、MS3DPrintUSB.inf ファイルで次の手順では、/*自動PnP を使用してドライバーのインストール*以下のセクション。

- 3D プリンターは試験段階の場合、または開発で、次の手順では、*ドライバーを手動でインストール*既存の COM ポートに出力する、G コードをファイルに印刷するのには、次のセクション。

MS_COMP_3DPRINT については、次を参照してください。[入門ガイド - Microsoft 標準のドライバーの 3D プリンター](https://docs.microsoft.com/windows-hardware/drivers/3dprint/microsoft-standard-driver-for-3d-printers-)します。

OS の記述子の詳細については、次を参照してください。 [USB デバイスの Microsoft OS ディスクリプター](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)します。

### <a name="automatic-installation-of-the-driver-via-pnp"></a>PnP を使用して、ドライバーの自動インストール

1.  デバイスに MSO 記述子またはサポートされているハードウェア ID (VID/PID) を持たない場合、新しい VID/PID 組み合わせに追加、MS3DPrintUSB\_{アーキテクチャ}\\MS3DPrintUSB.inf ファイルと高度な設定とドライバーを Windows の再起動署名の無効化します。 このオプションは、一時的にし、開発目的でのみ使用する必要があります。

2.  管理者特権でコマンド プロンプトから、これら 2 つのコマンドを実行します。

    ```console
    pnputil -a {PathToSDK}\Bin\MS3DPrintUSB_{architecture}\MS3DPrintUSB.inf
    pnputil -a {PathToSDK}\Bin\RenderFilters_{architecture}\MS3DPrinter.inf
    ```

3.  USB シリアル デバイスを接続します。 新しい**標準の 3D プリンター**でデバイスをインストールする必要があります**デバイスとプリンター**します。

### <a name="install-the-driver-manually"></a>ドライバーを手動でインストールします。

1.  検索で printmanagement.msc **Cortana**します。

    ![印刷の管理](images/g-code-1.png)

2.  展開**プリント サーバー**をマシンの名前を展開し、右クリックして**ドライバー**を選択し、**ドライバーを追加しています**.

    ![印刷の管理 ダイアログ](images/g-code-2.png)

3.  をクリックして**次**を選択します **(x64)**、 をクリックして**次へ**、順にクリックします**ディスク**します。

4.  RenderFiltersV4 に移動します\_x64 フォルダーの選択の MS3DPrinter.inf をクリックして**OK**します。

5.  をクリックして**OK**、 をクリックして**次へ**、順にクリックします**完了**。

6.  **Windows スタート**、型**デバイスとプリンター**します。

7.  クリックして**プリンターの追加**します。

    ![プリンターを追加します。](images/g-code-3.png)

8.  選択**たいプリンターが一覧にない**します。

    ![デバイスを追加します。](images/g-code-4.png)

9.  選択**手動設定でローカル プリンターまたはネットワーク プリンターを追加**、順にクリックします**次**します。

    ![手動設定でローカル プリンターまたはネットワーク プリンターを追加します。](images/g-code-5.png)

10. 選択**新しいポートを作成**選択**3D ポート**、ポートの種類をクリックし、 **[次へ]** します。

    ![新しいポートを作成します。](images/g-code-6.png)

11. ポート名を入力し、クリックして**OK**します。

    ![ポート名を入力します。](images/g-code-7.png)

12. クリックして**ディスクがある**.

    ![ディスクを搭載してください.](images/g-code-8.png)

13. SDK とクリックからジェネリック 3D 印刷ドライバーのバイナリ パッケージに参照**OK**します。

14. **[次へ]** をクリックします。

    ![プリンタ ドライバをインストールします。](images/g-code-9.png)

15. ここに 3D プリンター名を変更するには、する場合は (表示されます、プリンターの UI で)、順にクリックします **[次へ]**、順にクリックします**OK**に管理者として実行するコマンドを許可します。

    ![プリンター名を入力します。](images/g-code-10.png)

16. インストールが完了したら**完了**します。








