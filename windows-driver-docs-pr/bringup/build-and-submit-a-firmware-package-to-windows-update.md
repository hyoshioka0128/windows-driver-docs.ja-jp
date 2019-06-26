---
title: ファームウェア パッケージを構築して Windows Update (WU) に送信する
description: ファームウェア パッケージを構築して Windows Update (WU) に送信する
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 40d73866d11f451674744b2fcbb8e7676796234c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364593"
---
# <a name="build-and-submit-a-firmware-package-to-windows-update-wu"></a>ファームウェア パッケージを構築して Windows Update (WU) に送信する

ファームウェアの更新プログラムは、ドライバー パッケージとして配布される、ためデバイス ドライバー パッケージとして、同様の検証と署名プロセスに従います。

1. ドライバー パッケージの内容でのシステムでテスト (SUT) がインストールされているときに、デバイスは、必須の Windows ハードウェア ラボ キット (HLK) テストを渡す必要があります。 具体的にはテストされているファームウェアのテストがない場合は、最も妥当な代替手段を見つけてに応じて HLK パッケージと結果を送信します。

2. 次に、ドライバー パッケージを送信できます、[パートナー センター](https://partner.microsoft.com/dashboard)に署名するためです。

3. 署名済み後、ドライバー パッケージは、申請者が Windows Update (WU) 経由でのハードウェア ダッシュ ボードを発行するオプションが申請者に提供されます (ドライバーの配布機能を使用)。

使用して Windows Update への発行を行う、[ハードウェア ダッシュ ボード](https://partner.microsoft.com/dashboard)ドライバーの配布機能を使用します。

ドライバー パッケージの署名は、両方に署名する必要がある場合に、UEFI ファームウェアの署名と異なります。 署名は、ハードウェア ダッシュ ボードのファイル署名サービス機能を使用して使用します。 セキュリティのカタログを使用して配信される、ドライバー パッケージの署名は、UEFI に渡す前に firmware.bin の整合性を確認して、Windows によって使用されます。 Windows では、ファームウェアにセキュリティのカタログは提供されません。 UEFI ファームウェアまたはデバイスのファームウェア更新の署名は、プラットフォーム ファームウェアによって検証され、Windows ではチェックされません。 IHV および OEM は、整合性、および署名の検証、暗号化、またはその他の手段を介してファームウェアのセキュリティを確保します。 レビュー、[ポリシーの更新プログラムを Microsoft UEFI CA 署名](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)詳細については以下のリンクします。

ターミネータの内容を次に、サインインします。 Capsule コンテンツ自体は、OEM によって決定されます。 ターミネータは OEM 形式を選択で更新するファームウェア イメージのカタログを含めることができますだけまたは EFI アプリケーション イメージ (PE と COFF ファイル形式) の形式で届く場合があります。 ターミネータが PE と COFF ファイルの場合する必要があります署名する必要が、OEM が Microsoft Windows のファームウェア更新プログラム パッケージの署名に送信する前にします。

ARM ベースのシステムでは、キーなしでその他の UEFI 許可されているデータベースと Microsoft に許可されている Microsoft 運用 CA 2011 は、サード パーティ製 UEFI のコードの署名にこの CA で署名者を使いませんよりも、このような capsule の負荷を活用できません正規 UEFI **LoadImage()** サービス。 Capsule のアプリケーションがある可能性があります、ただし、ブート ROM の公開キーまたは UEFI の PK に対するプラットフォームに固有の検証を使用して読み込まれます TPM PCR にこの負荷を測定する必要がありますも\[7\]任意のイメージです。 (たとえば、完全な更新プログラム パッケージの整合性と信頼性を確認する) を必要と思われる capsule 署名と、ターミネータが外部での UEFI ファームウェアのファームウェアの更新プログラムを構成する場合があります、ターミネータが必要になることのような方法で署名プラットフォームの保持を使用して確認できます (たとえば、符号付きを使用してブート ROM または UEFI の PK にバインドされている公開キーにキーの組み合わせ) 非 UEFI キー。

![ドライバーの署名のワークフロー](images/driver-signing-workflow.png)

ARM 以外のシステムでは、

- ターミネータは、UEFI 許可されているデータベース内のエントリにキー チェーンで署名されている限り、EFI アプリケーションにすることができます。

- UEFI セキュア ブートし、自動的に活用すること、capsule の整合性を検証します。

> [!NOTE]
> Windows では、テスト環境であっても OEM Verisign 署名されたファームウェア更新プログラム パッケージは許可されません。 Microsoft によって署名されて、ポータルでテストする必要があります。

ファームウェアの更新プログラム パッケージをインストールすることによって、SUT デバイスのファームウェアを更新します。

テスト システム、PTP で Windows ハードウェア ラボ キット (HLK) をインストールし、ファームウェアのデバイスに適用可能なすべてのテストを実行します。送信、 *HLK ログと、ドライバー パッケージ*署名のためのパートナー センターにします。

> [!NOTE]
> ファームウェアの更新プログラムのドライバー パッケージを送信中に、該当する OS として Windows 8 以降を選択してください。 すべてのダウンレベルの OS を選択した場合、パートナー センターは SHA1 アルゴリズムでドライバー パッケージ内のカタログを署名します。 Windows 8 以降、ファームウェア更新のすべてのドライバー パッケージは SHA256 署名をする必要があります。

、推奨されませんが、HLK テスト ログを生成する (またはしない HLK テスト ログを送信するときなど) には、Microsoft にパッケージを送信することです。 使用**作成ドライバーの送信を署名**HLK パス テスト ログをせずに、または検証をテストするためにドライバーが署名するためです。

ドライバーは HLK テスト ログなしで署名の要件は、ドライバーが CAB 形式で送信されることです。

インボックス Makecab.exe は、CAB ファイルを作成できます。 使用可能な (Cabarch.exe) などの他のツールは、することがありますの詳細は見つけにくい、ボックスに含まれていません。

キーは、CAB ファイルにも、ドライバーを含むフォルダーが含まれているかどうかを確認します。 たとえば、ドライバー パッケージには、次のような構造があります。

```syntax
C:\Desktop
        \DriverFolderOne
                Driver.inf
                Driver.sys
```

この形式に従うと、送信は渡す必要があります。 Cab ファイルに組み込まれた親フォルダーを確認するには、するには、Windows エクスプ ローラーとスイッチで cab ファイルを開きます**ビュー**に**詳細**します。 **パス**列は空にできません。

## <a name="related-resources"></a>関連リソース

[ファームウェアの更新プログラム パッケージの作成](https://docs.microsoft.com/windows-hardware/drivers/bringup/authoring-a-firmware-update-package)

[認定と更新プログラム パッケージの署名](https://docs.microsoft.com/windows-hardware/drivers/bringup/certifying-and-signing-the-update-package)

[Device.Fundamentals の信頼性テストの前提条件](https://docs.microsoft.com/windows-hardware/test/hlk/testref/devicefundamentals-reliability-testing-prerequisites)

[ドライバーの署名](https://docs.microsoft.com/windows-hardware/drivers/dashboard)

[Microsoft UEFI CA 署名ポリシーの更新](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)

[テスト結果を表示し、ログ ファイル](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/step-7-view-test-results-and-log-files)

[提出パッケージを作成します。](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/step-8-create-a-submission-package)

[ファームウェアのドライバー パッケージを使用してシステムとデバイスのファームウェア更新プログラム](https://docs.microsoft.com/windows-hardware/drivers/bringup/system-and-device-firmware-updates-via-a-firmware-driver-package)

[Windows HLK を使用した Device Fundamentals 信頼性テストのトラブルシューティング](https://docs.microsoft.com/windows-hardware/test/hlk/testref/troubleshooting-device-fundamentals-reliability-testing-by-using-the-windows-hck)

[Windows ハードウェア認定のブログ](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)

[Windows の UEFI ファームウェアを更新するプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-uefi-firmware-update-platform)

[パートナー センター](https://partner.microsoft.com/dashboard)

[ESRT テーブルの定義 ](https://docs.microsoft.com/windows-hardware/drivers/bringup/esrt-table-definition)
