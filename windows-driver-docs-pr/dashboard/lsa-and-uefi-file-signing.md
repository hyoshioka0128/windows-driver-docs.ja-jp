---
title: LSA/UEFI ファイル署名
description: LSA プラグインと UEFI ファームウェアの署名
ms.localizationpriority: medium
ms.topic: article
ms.date: 10/17/2018
ms.openlocfilehash: 10235b66c1578e56c70f106b2d1bec592764d512
ms.sourcegitcommit: a678a339f09fbd56a3a6124c0fe86194fedb2ed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2019
ms.locfileid: "57560587"
---
# <a name="file-signing-lsa-plugins-and-uefi-firmware"></a>LSA プラグインと UEFI ファームウェアのファイル署名

パートナー センターを使用して、[ローカル セキュリティ機関 (LSA)](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/configuring-additional-lsa-protection)のプラグインと [UEFI ファームウェア](https://docs.microsoft.com/windows-hardware/design/device-experiences/oem-uefi)のバイナリへデジタル署名し、これらを Windows デバイスにインストールできるようにします。

> [!IMPORTANT]
> このトピックで説明されているファイル署名手法は、**UEFI** と **LSA** の署名に使用します。
> **ドライバー**署名について詳しくは、[ハードウェア申請](https://docs.microsoft.com/windows-hardware/drivers/dashboard/hardware-certification-submissions)に関する記事をご覧ください。
>
> * ファイル署名には、[拡張検証 (EV) コード署名証明書](get-a-code-signing-certificate.md)が必要です。
> * すべての LSA 申請および UEFI 申請は、署名に必要なファイルをすべて含めて、署名済みの 1 つの CAB ライブラリ ファイルにまとめる必要があります。
>   * このファイルには、フォルダーを含めず、署名対象のバイナリまたは .efi ファイルのみを含める必要があります。
> * **UEFI ファームウェアの場合のみ**: CAB ファイル署名が組織の [Authenticode 証明書](https://docs.microsoft.com/windows-hardware/drivers/install/authenticode)に一致する必要があります。
>   * 証明書プロバイダーによっては、[SignTool](https://msdn.microsoft.com/library/windows/desktop/aa387764) または外部プロセスの使用が必要になる場合があります。
>   * 処理が正常に行われるようにするには、EFI ByteCode (EBC) ファイルを、/ALIGN:32 フラグを使ってコンパイルする必要があります。
> * **UEFI ファームウェアの場合のみ**: 申請が shim の場合は、完成済みのテンプレートを shim レビュー委員会に提出する必要があります。 shim のレビュー プロセスについては、[https://github.com/rhboot/shim-review/](https://github.com/rhboot/shim-review/) で説明されています。
> **LSA プラグインの場合のみ**: CAB ファイル署名が組織の EV コード署名証明書に一致する必要があります。

## <a name="creating-a-new-uefi-or-lsa-submission"></a>新しい UEFI 申請または LSA 申請の作成

1. Microsoft アカウントでダッシュボードにサインインして、**[ハードウェア認定]** をクリックします。

2. **[ファイル署名サービス]** ページで、**[Submit New UEFI]** (新しい UEFI の申請) または **[Submit New LSA]** (新しい LSA の申請) をクリックします。
    > [!NOTE]
    > 新しいファイル署名申請を作成する前に、法的契約への署名を求めるメッセージが表示される場合があります。 契約内容を確認し、同意して続行します。 組織はすべて、契約に 1 回だけ署名する必要があります。

3. 申請ページで、提出する CAB ファイルをアップロードし、**[送信]** をクリックします。

4. 申請が処理されると、申請 ID が含まれた通知が送られて来ます。

## <a name="managing-your-file-signing-submission"></a>ファイル署名申請の管理

パートナー センターにログインした後、他のダッシュボード申請と同様に、[ファームウェア申請を管理](manage-your-hardware-submissions.md)することができます。

## <a name="related-topics"></a>関連トピック

* [Microsoft UEFI CA の署名ポリシーが更新されました](http://blogs.msdn.com/b/windows_hardware_certification/archive/2013/12/03/microsoft-uefi-ca-signing-policy-updates.aspx)

* [UEFI サブミッションのサブミッション事前テスト](http://blogs.msdn.com/b/windows_hardware_certification/archive/2013/12/03/pre-submission-testing-for-uefi-submissions.aspx)
