---
title: CHID ターゲットを使用してシステムをターゲットにする
description: CHID ターゲットを使用してシステムをターゲットにする
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 15c0d6205624d3bb2a3ca8a104d1a6e6f6187eb4
ms.sourcegitcommit: 1585a52e762226b01c7369371727746487cc57bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74796662"
---
# <a name="target-a-system-using-chid-targeting"></a>CHID ターゲットを使用してシステムをターゲットにする

コンピューターのハードウェア Id (CHID) は、Windows Developer Kit (WDK) ツール (Computerhardware Ids .exe) を実行している OEM/ODM、または[MICROSOFT oem ダウンロードサイト](https://www.microsoftoem.com)(ログインが必要) を通じて oem が利用できる監査ツールで作成されます。

CHIDs はコンピューターのハードウェア Id であり、Windows では、これらの Id をさまざまなレベルでターゲットとして使用します。 正しいドライバーがシステムに配布されると、「 [Windows がドライバーをランク](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)付けする方法」で説明されているように、通常の PNP 順位が引き継がれます。また、ベンダーは、製品ラインに適した方法を構築できます。

OEM/ODM は、 [smbios](smbios.md)ガイダンスに記載されている情報に基づいて、すべての適切な smbios フィールドにデータが設定されていることを確認する必要があります。また、chids が個人で一意であることを保証するために、 [DMTF の smbios 仕様](https://www.dmtf.org/standards/smbios)に従ってください。

Microsoft では、EFI システムリソーステーブル (ESRT) の **[システム]** に表示されている一意の id に加えて、ファームウェア更新パッケージにコンピューターハードウェア ID (chid) を含めるように要求しています。 「 [Windows 10 用ドライバー公開ワークフローのダウンロード](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)」ドキュメントには、配布のターゲット設定とインストールの対象で使用される chids の詳細な説明が含まれています。

## <a name="related-resources"></a>関連リソース

[パートナー センター](https://docs.microsoft.com/windows-hardware/drivers/dashboard)

[コンピューターのハードウェア Id の指定](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer)

[Windows 10 用のドライバー発行ワークフローのダウンロード](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)
