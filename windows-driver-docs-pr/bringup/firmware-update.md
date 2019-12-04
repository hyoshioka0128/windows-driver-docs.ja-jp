---
title: ファームウェアの更新
description: Microsoft Windows Update (WU) と UEFI UpdateCapsule 機能を使用して、システムとデバイスのファームウェアの更新プログラムを配信するためのサポートについて説明します。
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed5adef3f3fb2debd0c9a6f1d5e3bd2e5830a971
ms.sourcegitcommit: 1585a52e762226b01c7369371727746487cc57bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74796666"
---
# <a name="firmware-update"></a>ファームウェアの更新

Windows は、Microsoft Windows Update (WU) を使用して配布されたドライバーパッケージにラップされたシステムおよびデバイスのファームウェアの更新プログラムを配信するためのプラットフォームをサポートしており、UEFI **UpdateCapsule**関数に渡されて処理されます。 このプラットフォームにより、一貫性のある信頼性の高いファームウェアの更新エクスペリエンスが提供され、エンドユーザーにとって重要なシステムファームウェアの更新プログラムを配信する機能が向上します。

この機能は、Windows 8.1 の早い段階で利用できるようになりました。 ただし、最近の変更によっては、特定のシステムまたはシステム範囲をより正確にターゲットにするために、ファームウェアプロバイダーがコンピューターハードウェア ID (CHID) をモデル固有の EFI システムリソーステーブル (ESRT) UEFI\_RES\\{一意 ID} と組み合わせる必要があります。

ESRT の一意の ID {一意の ID} が重要です。 一意の ID + CHID の目的は、ファームウェアプロバイダーが、一意の ID + CHID と一致するすべてのシステムに Windows Update (WU) を介して展開されるファームウェア更新パッケージ/BIOS を作成できるようにするためです。 Microsoft には、ファームウェアパッケージを検証するメカニズムがありません。また、ペイロードが改ざんされていないことを確認するために、ファームウェアプロバイダー (パッケージの作成者) に依存しています。 暗号化を検証する必要があります。チェックサムまたはその他の CRCs は検証されません。 ペイロードが検証に失敗した場合、「 [esrt テーブルの定義](https://docs.microsoft.com/windows-hardware/drivers/bringup/esrt-table-definition)」で説明されているように、失敗して esrt に状態を記録する必要があります。

> [!NOTE]
> ESRT {一意 ID} を設定しようとした OEM、ODM、または担当者が ESRT に {Unique ID} が事前に設定されていることを検出する場合は、これが一意であると想定しないでください。 ESRT に {一意 ID} を設定し、後で使用するためにこのレコードを記録します。 これらのシナリオでは、Microsoft が一意の ID を作成する方法についてのガイダンスを示しています。 このガイドは、 [Windows 10 のドライバー発行ワークフロー](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)のダウンロード可能なドキュメントに記載されています。

## <a name="in-this-section"></a>このセクションの内容

[ファームウェアパッケージをビルドして Windows Update (WU) に送信する](build-and-submit-a-firmware-package-to-windows-update.md)

[CHID を使用してシステムをターゲットにする](target-a-system-using-chid.md)

[ファームウェアユーザーエクスペリエンス (UX) のベストプラクティス](firmware-user-experience-best-practices.md)

[ファームウェア更新の検証テスト](firmware-update-validation-testing.md)
