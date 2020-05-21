---
title: 3D 印刷パートナー オンボーディング ガイド
description: このトピックでは、Windows Update で公開された3D プリンタードライバーを実装する方法について説明します。
ms.date: 05/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5bf0c671a5878bb93e375c967fdb5527fa93759c
ms.sourcegitcommit: 32f42241991d57032e5d39ee9f2a3ab4a66ae396
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/18/2020
ms.locfileid: "83553331"
---
# <a name="3d-print-partner-onboarding-guide"></a>3D 印刷パートナー オンボーディング ガイド

Microsoft 3D 印刷エコシステムに参加することで、3D プリンターの製造元は Windows 10 で優れたプラグアンドプレイエクスペリエンスを実現できます。 この方法を使用すると、ドライバーを検索して手動でインストールするときに発生する問題の可能性を排除できます。 さらに、Windows Update によって、ユーザーは常に最新のドライバーを使用してデバイスを使用できるようになり、最適なエクスペリエンスが得られます。

## <a name="3d-print-driver-overview"></a>3D 印刷ドライバーの概要

Windows 10 でプラグアンドプレイ3D プリンターを実装するには Windows Update で公開されているドライバーのペアを使用します。

### <a name="upper-driver-render-filter"></a>上位ドライバー (レンダリングフィルター)

- スライサーを実装します。 ドライバーは、入力として[3Mf](https://3mf.io/)を受け取り、G コードまたはその他の同様のマシンレベルデータを生成します。

- 印刷キューを作成します。 デバイスは、互換性のある[3D 印刷アプリケーション](https://developer.microsoft.com/windows/hardware/3d-print/software-partners)の [**デバイスとプリンター** ] および [ **3d 印刷] ダイアログ**の下に表示されます。

### <a name="lower-driver-usb-driver"></a>下位ドライバー (USB ドライバー)

- ワイヤプロトコル (通常は USB シリアルまたはネイティブ USB) を実装します。

- カーネルモードドライバーは、 \\ 上位ドライバーの列挙型3dprinter デバイスノードを作成します。

- ユーザーモードコンポーネント (パートナー DLL) は、G コードをデバイスに送信します。

- デバイスの機能、ジョブの状態を報告し、ジョブのキャンセルを実装します

- 3D 印刷サービスと3D ポートモニター (3dmon) をインストールします。

## <a name="choosing-the-right-driver-model"></a>適切ドライバーモデルの選択

![次のセクションで説明するように、上位および下位のドライバーの Microsoft およびカスタム3D ドライバーモデルの長所と短所を示す4×4のグリッド](images/onboarding-driver-models.png)

## <a name="3d-print-driver-with-custom-slicer"></a>カスタムスライサーを使用した3D 印刷ドライバー

1. デバイスの USB ハードウェア ID を取得して確認する

    - デバイスのファームウェアに、 [Usb 実装者フォーラム (USB IF)](https://www.usb.org/)によって割り当てられた一意のベンダ Id と製品 ID (VID/PID) があることを確認します。 USBSER デバイスでは、USB ポートの変更による競合を防ぐために、一意のシリアル番号を使用することを強くお勧めします。

2. Microsoft のツールと Sdk をインストールする

    - [Visual Studio Community Edition](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community)をダウンロードしてインストールする

    - [Windows 10 SDK](https://developer.microsoft.com/en-US/windows/downloads/windows-10-sdk/)のダウンロードとインストール

    - [3d 印刷 SDK](https://go.microsoft.com/fwlink/p/?LinkId=394375)のダウンロードとインストール

   > [!NOTE]
   > 3D 印刷 SDK は、C: \\ Program Files (x86) \\ Microsoft Sdk 3d 印刷にインストールされ \\ ます。

3. USB ドライバーを実装する

    - 製造元は、パートナー DLL を作成することによって、3D プリンターに Microsoft USB ドライバーを使用できます。 詳細については、「 [3d プリンターカスタム USB インターフェイスのサポート](3d-printer-custom-usb-interface.md)」を参照してください。

    - プリンターが Microsoft スライサーを使用している場合は、作成するハードウェア ID が**列挙型 \\ 3dprint \\ MS3DPrint**である必要があります。

    > [!NOTE]
    > プリンターがカスタムスライサーを使用している場合は、手順4-7 に進みます。

4. Fabrikam ドライバーのビルド (スライサーテンプレートのみ)

    - ドライバーパッケージをビルドして取得します。 これにより、スライサー部分を含む x64 フォルダーが作成されます。

5. カスタムスライサーの追加

    - Cpp ファイルを次のように変更します。

      - 3MF パーサー (Windows 10 バージョン 1607 3MF API を使用)

      - G コードを記述する

6. プリンターノードの追加

    - Fabrikam Print driver で inf を開きます。

    - エントリのハードウェア Id を置き換えます。

        ```INF
        %DeviceName%=FabrikamPrintDriverV4\_Install,3DPRINTER\\Fabrikam1

        %DeviceNamePlus%=FabrikamPrintDriverV4\_Install,3DPRINTER\\Fabrikam2

        DeviceName="CONTOSO FABRIKAM 1"

        DeviceNamePlus="CONTOSO FABRIKAM 2"
        ```

7. ドライバーの発行と配布

    - [Windows パートナーセンター](https://docs.microsoft.com/windows-hardware/drivers/dashboard)のトピックに記載されているガイダンスに従って、ドライバーを発行します。
