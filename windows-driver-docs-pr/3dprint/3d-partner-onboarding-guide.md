---
title: 3D 印刷パートナー オンボーディング ガイド
description: このトピックでは、Windows Update にし、公開されている 3D プリンター ドライバーを実装する方法について説明します。
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0a923651df76199d8ff6179c1475c271ebad2e33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323536"
---
# <a name="3d-print-partner-onboarding-guide"></a>3D 印刷パートナー オンボーディング ガイド

Microsoft 3D 印刷エコシステムに参加する Windows 10 で優れたプラグ アンド プレイ エクスペリエンスを提供する 3D プリンターの製造元を使用できます。 この戦略では、ユーザーを検索して、ドライバーを手動でインストールするときに発生する問題の可能性を削除します。 さらに、Windows Update はにより、ユーザーが自分のデバイスの最新のドライバーを使用して常にいるし、使用可能な最適なエクスペリエンスを取得することです。

## <a name="3d-print-driver-overview"></a>3D 印刷ドライバーの概要

Windows 10 でプラグ アンド プレイの 3D プリンターは、Windows Update に公開されたドライバーのペアを通じて実装されます。

### <a name="upper-driver-render-filter"></a>上のドライバー (レンダー フィルター)

- スライサーを実装します。 ドライバーは[3MF](http://www.3mf.io)として入力し、G コードまたはその他のようなマシン レベルのデータを生成します。

- 印刷キューを作成します。 下に、デバイスが表示されます**デバイスとプリンター**し、 **3D 印刷ダイアログ**の互換性のある[3D 印刷アプリケーション](https://developer.microsoft.com/windows/hardware/3d-software-partners)します。

### <a name="lower-driver-usb-driver"></a>下位のドライバー (USB ドライバー)

- 実装のワイヤ プロトコル (通常の USB シリアルまたはネイティブの USB)

- カーネル モード ドライバーは、列挙型を作成します\\3DPRINTER 上のドライバーの [デバイス] ノード。

- ユーザー モード コンポーネント (パートナー DLL)、G コードをデバイスに送信します。

- レポートのデバイス機能、ジョブの状態と実装のジョブのキャンセル

- 3D 印刷サービスと、3 D ポート モニター (3dmon を) インストールします。

## <a name="choosing-the-right-driver-model"></a>適切なドライバー モデルの選択

![4 x 4 グリッドの上の Microsoft およびカスタムの 3D ドライバー モデルの長所と短所を表示するように、次のセクションで説明されているドライバーを減らす](images/onboarding-driver-models.png)

## <a name="3d-print-driver-with-custom-slicer"></a>スライサーをカスタムの 3D 印刷ドライバー

1. 取得し、デバイスの USB ハードウェア ID を確認します

    - デバイスのファームウェアが、一意のベンダー ID と製品 ID (PID/VID) によって割り当てられたことを確認、 [USB Implementers Forum (USB の場合)](http://www.usb.org)します。 USBSER デバイスでは、ことをお勧め、USB 上の競合を回避する一意のシリアル番号を使用するポートの変更。

2. Microsoft ツールおよび Sdk をインストールします。

    - ダウンロードしてインストール[Visual Studio Community エディション](https://go.microsoft.com/fwlink/p/?LinkId=534599)

    - ダウンロードしてインストール、 [Windows 10 SDK](https://go.microsoft.com/fwlink/p/?LinkID=822845)

    - ダウンロードしてインストール、 [3D 印刷 SDK](https://go.microsoft.com/fwlink/p/?LinkId=394375)

   > [!NOTE]
   > 3D 印刷 SDK は c: でインストールする\\Program Files (x86)\\Microsoft SDKs\\3D 印刷します。

3. USB ドライバーを実装します。

    - 製造元は、パートナーの DLL を作成して、自社の 3D プリンター用 Microsoft USB ドライバーを使用できます。 詳細については、次を参照してください。[カスタム USB インターフェイスのサポートの 3D プリンター](3d-printer-custom-usb-interface.md)します。

    - プリンターは、Microsoft のスライサーで使用されている場合、作成したハードウェア ID がある必要があります**Enum\\3DPrint\\MS3DPrint**

    > [!NOTE]
    > プリンターは、カスタムのスライサーで使用されている場合は、手順 4 ~ 7 に進みます。

4. Fabrikam ドライバー (スライサー テンプレートのみ)

    - 構築し、ドライバー パッケージを取得します。 こうと、x64、スライサーの一部のフォルダー。

5. カスタムのスライサーを追加します。

    - 含めるよう、cpp ファイルを変更します。

      - 3MF パーサー (Windows 10 バージョン 1607 3MF API を使用)

      - G コードを記述します。

6. プリンターのノードを追加します。

    - Fabrikam の印刷ドライバーの inf ファイルを開く

    - エントリのハードウェア Id に置き換えます。

        ```INF
        %DeviceName%=FabrikamPrintDriverV4\_Install,3DPRINTER\\Fabrikam1

        %DeviceNamePlus%=FabrikamPrintDriverV4\_Install,3DPRINTER\\Fabrikam2

        DeviceName="CONTOSO FABRIKAM 1"

        DeviceNamePlus="CONTOSO FABRIKAM 2"
        ```

7. 公開し、ドライバーの配布

    - ガイダンスに従って、 [Windows パートナー センター](https://docs.microsoft.com/windows-hardware/drivers/dashboard)トピックには、ドライバーを発行します。
